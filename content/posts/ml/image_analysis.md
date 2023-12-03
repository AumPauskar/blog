+++
title = 'Image analysis with pytorch'
date = 2023-12-03T20:40:58+05:30
draft = false
+++

# Image Analysis using pytorch

## Prerequisites
This project is built using python in Ubuntu (WSL) and you'll need to install the following:
1. Any bash terminal (one of the following)
	- Conda
	- WSL
	- Mac OS
	- Any flavour of Linux
2. Python 3 (I'm using 3.10.12)
	```bash
	sudo apt update
	sudo apt install python3
	```
3. Pip
	```bash
	sudo apt update
	sudo apt install python3-pip
	```
4. Packages \
	**Note:** Since I'm using a computer with a CUDA compatable NVIDIA GPU, I'll be using the GPU version of pytorch. If you don't have a GPU, you can install the CPU version of pytorch given below.
	- CPU install
		```bash
		pip3 install torch torchvision numpy matplotlib
		```
	- GPU install \
		Installing numpy and matplotlib
		```bash
		pip3 install numpy matplotlib
		```
		Installing pytorch \
		Check the [pytorch website](https://pytorch.org/get-started/locally/) to see the which library is compatable with your system. \
		In my case I'm using CUDA 11.8
		```bash
		pip3 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118
		```
5. Jupyter notebook (optional)
	```bash
	pip3 install jupyterlab
	```
	Or just use Jupyter notebook from VS Code [from here](https://code.visualstudio.com/docs/datascience/jupyter-notebooks)

### Environement I've used
|  |  |  |
| --- | --- | --- |
| 1 | CPU | Ryzen 7 5800H |
| 2 | GPU | RTX 3060 Laptop |
| 3 | RAM | 2x8GB DDR4 @ 3200MHz |
| 4 | OS | Windows 11/Ubuntu 22.4 WSL |
| 5 | CUDA | 11.8 |
| 6 | Python | 3.10.12 |

## MNIST Dataset
The MNIST dataset is a dataset of handwritten digits. It has 60,000 training images and 10,000 test images. We'll see a code to load the dataset and display the occurances of individual digits in the dataset. Or if you want to run the code from Jupyter notebook you can clone my repository via git.
```bash
git clone https://github.com/AumPauskar/biomed-image-analysis.git
cd mnist/
```

RAW code
```py
import torch
import torch.nn as nn
import torch.nn.functional as F
from torchvision import datasets, transforms
from torch.utils.data import DataLoader
import numpy as np

# Load the MNIST dataset
mnist_dataset = torchvision.datasets.MNIST(root='./data', train=True, transform=None, target_transform=None, download=True)

# Get the first image from the dataset
image, label = mnist_dataset[0]

# Check if CUDA is available
device = torch.device("cuda" if torch.cuda.is_available() else "cpu")

# Step 2: Load the MNIST dataset
transform = transforms.ToTensor()

train_data = datasets.MNIST(root='./data', train=True, download=True, transform=transform)
test_data = datasets.MNIST(root='./data', train=False, download=True, transform=transform)

train_loader = DataLoader(train_data, batch_size=200, shuffle=True)
test_loader = DataLoader(test_data, batch_size=200, shuffle=False)

# Step 3: Define the CNN model
class ConvNet(nn.Module):
    def __init__(self):
        super(ConvNet, self).__init__()
        self.conv1 = nn.Conv2d(1, 32, 5)
        self.fc1 = nn.Linear(12*12*32, 128)
        self.fc2 = nn.Linear(128, 10)

    def forward(self, x):
        x = F.relu(self.conv1(x))
        x = F.max_pool2d(x, 2, 2)
        x = x.view(-1, 12*12*32)
        x = F.relu(self.fc1(x))
        x = self.fc2(x)
        return x

model = ConvNet().to(device)  # Move the model to GPU

# Step 4: Define the loss function and optimizer
criterion = nn.CrossEntropyLoss()
optimizer = torch.optim.Adam(model.parameters(), lr=0.001)

# Step 5: Train the model
for epoch in range(10):
    for i, (images, labels) in enumerate(train_loader):
        images = images.to(device)  # Move the images to GPU
        labels = labels.to(device)  # Move the labels to GPU

        outputs = model(images)
        loss = criterion(outputs, labels)
        
        optimizer.zero_grad()
        loss.backward()
        optimizer.step()

# Step 6: Evaluate the model
model.eval()
with torch.no_grad():
    correct = 0
    total = 0
    for images, labels in test_loader:
        images = images.to(device)  # Move the images to GPU
        labels = labels.to(device)  # Move the labels to GPU

        outputs = model(images)
        _, predicted = torch.max(outputs.data, 1)
        total += labels.size(0)
        correct += (predicted == labels).sum().item()

    print('Test Accuracy: {} %'.format(100 * correct / total))

# Step 7: Predict on the test data and count the occurrences of each digit
with torch.no_grad():
    all_predicted = []
    for images, labels in test_loader:
        images = images.to(device)  # Move the images to GPU

        outputs = model(images)
        _, predicted = torch.max(outputs.data, 1)
        all_predicted += predicted.tolist()

(unique, counts) = np.unique(all_predicted, return_counts=True)
frequencies = np.asarray((unique, counts)).T
print(frequencies)
```

**CPU version:** ~ 3.1 mins \
**CUDA version:** ~ 55 secs