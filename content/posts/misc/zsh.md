+++
title = 'ZSH configuration'
date = 2023-12-20T06:58:03+05:30
draft = false
+++

# ZSH configuration
ZSH is a shell designed for interactive use, although it is also a powerful scripting language. Many of the useful features of bash, ksh, and tcsh were incorporated into zsh; many original features were added.

## Installation
1. Update and install
	ZSH can be installed on any linux based system using the following command:

	```bash
	sudo apt update
	sudo apt install zsh -y
	```

	This will update the system binaries and install the zsh shell on the system.

	```bash
	zsh --version
	```

	This command will give you the version of zsh installed on the system and verify the installation.

2. Change default shell
	```bash
	zsh
	chsh -s $(which zsh)
	source ~/.zshrc
	```

3. install On My ZSH
	On My ZSH is a framework for managing your ZSH configuration. It includes many useful plugins, themes, and helpers.
	```bash
	sh -c "$(wget https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh -O -)"
	```

4. Install syntax highlighting and autosuggestions
	```bash
	git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions

	git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
	```

5. Enable extensions

	Open the `zshrc` file
	```bash
	nano ~/.zshrc
	```

	Add (or replace) this line in the `zshrc` file
	```bash
	plugins=(git zsh-autosuggestions zsh-syntax-highlighting)
	```