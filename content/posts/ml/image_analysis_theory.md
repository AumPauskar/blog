+++
title = 'Image analysis theory'
date = 2023-12-06T00:12:10+05:30
draft = false
tags = ["machine learning", "image processing", "ai", "computer vision", "python"]
author = "Aum Pauskar"
description = "A brief overview of image processing and machine learning concepts."
+++

# Image processing

## Theory jargon
### Difference between supervised and unsupervised learning
| Criteria | Supervised Learning | Unsupervised Learning |
| --- | --- | --- |
| Data | Uses labeled data for training. | Uses unlabeled data for training. |
| Goal | Predict a label for new data based on past observations. | Discover hidden patterns or intrinsic structures within the data. |
| Examples | Classification, Regression | Clustering, Association |
| Complexity | Less complex as it has a clear goal. | More complex due to the lack of clear goal. |
| Usage | When the outcome of the problem is known. | When the outcome of the problem is unknown. |
| Application #1 | Spam Detection | Customer Segmentation |
| Application #2 | Credit Fraud Detection | Anomaly Detection |

### EM spectrum
The Electromagnetic Spectrum (EM) is the range of all types of EM radiation. Radiation is energy that travels and spreads out as it goes – visible light that comes from a lamp in your house or radio waves from a radio station are two types of electromagnetic radiation. Other examples of EM radiation are microwaves, infrared and ultraviolet light, X-rays, and gamma-rays.

In the context of image processing, the EM spectrum is significant because different types of EM radiation can be used to capture different types of images. For example, X-rays can be used to capture images of bones and internal body structures, while visible light can be used to capture everyday photographs.

Image resolution refers to the detail an image holds and can be defined in various ways, including pixel resolution, spatial resolution, spectral resolution, etc. Higher resolution means more image detail.

Here's a comparison of three different resolutions for specific applications:

Low Resolution (e.g., 640x480): Suitable for web images, thumbnails, or any application where storage space is a premium and high detail is not necessary.

Medium Resolution (e.g., 1280x720): Suitable for video streaming, online gaming, or any application where a balance between detail and performance is necessary.

High Resolution (e.g., 3840x2160): Suitable for professional photo editing, 4K video editing, or any application where high detail is necessary and storage space/performance is not a concern.

The significance of different resolutions depends on the specific application. Higher resolutions provide more detail but require more storage space and processing power. Therefore, the optimal resolution depends on the specific requirements of the application.

### Image processing
- Image acquisition
- Image restoration
- Image enhancement
	- Image compression
	- Image encryption
- Image segmentation
- Feature extraction
- Recognition/interepretation

### MNIST dataset
The MNIST (Modified National Institute of Standards and Technology) dataset is a large database of handwritten digits that is commonly used for training and testing in the field of machine learning. It contains 60,000 training images and 10,000 testing images, each of which is a 28x28 grayscale image of a digit between 0 and 9.

The significance of the MNIST dataset lies in its use as a benchmark for evaluating the performance of machine learning algorithms. It's a relatively simple dataset that allows researchers and developers to try out new algorithms and techniques without the need for complex data preparation. It's often one of the first datasets that those new to machine learning will work with. Despite its simplicity, achieving high accuracy on MNIST is still a challenge, making it a useful stepping stone to more complex image recognition tasks.

#### Strategic decisions involving in training of the MNIST dataset
Designing and fine-tuning an Artificial Neural Network (ANN) for classifying handwritten digits on the MNIST dataset involves several significant components and strategic decisions:

1. Network Architecture: The first decision is choosing the architecture of the neural network. For the MNIST dataset, a simple feed-forward neural network can work well, but a Convolutional Neural Network (CNN) might give better results as they are designed to recognize patterns in images.
2. Number of Layers and Neurons: The number of layers and neurons in each layer is a critical decision. Too few may result in underfitting, while too many can lead to overfitting.
3. Activation Function: The activation function introduces non-linearity into the network. Common choices are ReLU, sigmoid, and tanh.
4. Loss Function: Since MNIST is a multi-class classification problem, a common choice for the loss function is Cross-Entropy Loss.
5. Optimizer: The optimizer adjusts the weights of the network to minimize the loss. Common choices are SGD, Adam, and RMSprop.
6. Learning Rate: The learning rate controls how much to change the model in response to the estimated error each time the model weights are updated. Choosing the learning rate is challenging as a value too small may result in a long training process, whereas a value too large may result in learning a sub-optimal set of weights.
7. Batch Size: The batch size is the number of samples that will be passed through to the network at one time. Larger batch sizes result in faster progress in training, but don't always converge as fast. Smaller batch sizes train slower, but can converge faster.
8. Epochs: The number of epochs is the number of times the learning algorithm will work through the entire training dataset.
9. Regularization: Techniques like dropout or L1/L2 regularization can be used to prevent overfitting.
10. Data Augmentation: Techniques such as rotation, shifts, and flips can help to increase the amount of training data and improve the model's performance.

Remember, the process of fine-tuning these parameters is often empirical and requires several iterations to find the optimal configuration.

#### Case study - ANN for malignant tissues
Implementing an Artificial Neural Network (ANN) for identifying benign and malignant tissues in digital whole slide images of colon tissues involves several key steps:

1. Data Collection: Collect a large number of whole slide images of colon tissues that have been labeled as benign or malignant by pathologists.
2. Preprocessing: Preprocess the images to a suitable size and format for the neural network. This may involve resizing, normalization, and augmentation techniques to increase the diversity of the training data.
3. Network Architecture: Choose an appropriate network architecture. Convolutional Neural Networks (CNNs) are often used for image classification tasks due to their ability to capture spatial information.
4. Training: Train the network on the preprocessed images. This involves feeding the images into the network, calculating the difference between the network's prediction and the actual label (the loss), and updating the network's weights to minimize the loss.
5. Validation: Validate the model's performance using a separate set of images that were not used during training. This helps ensure that the model is not overfitting to the training data.
6. Testing: Test the model on a completely new set of images to evaluate its performance.
7. Fine-tuning: Based on the results of validation and testing, fine-tune the model by adjusting its architecture, learning rate, batch size, number of epochs, etc.
8. Deployment: Once the model is performing well, it can be deployed in a clinical setting to assist pathologists in identifying benign and malignant tissues.