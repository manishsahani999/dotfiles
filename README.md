# Hades
Tooling is hard! and necessary. This is the way I like to configure my system. 

### Compilers, Language support and MacOS SDK 
First thing we need to do is get the language support, compilers and stuff. If you on MacOS, the easiest if to download and install `Xcode/Xcode Command Line`. I prefer xcode command line tools because I use `vim` and `vscode` for code editors and rarely need an IDE, and the biggest of all XCode is around 8GB.

The Xcode Command Line Tools Package is a small self-contained package available for download separately from Xcode and that allows us to do command line development in macOS. It consists of the macOS SDK and command-line tools, which are installed in the `/Library/Developer/CommandLineTools`.

```bash 
xcode-select --install
```

### Package Manager - Homebrew
For installing libraries and apps, I use [brew](https://brew.sh/) - The Missing Package Manager for MacOS. The installation is simple but requires `xcode-select` to be pre-installed.

```bash 
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```

### NVM, Nodejs, NPM and Yarn
[nvm](https://github.com/nvm-sh/nvm#about) is node version manager, works with any POSIX-compilant shell. To install or update nvm, you should run the install script. Following is the cURL command to download and run the install script.

```bash 
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.3/install.sh | bash
```
verify the installation of nvm using `command -v nvm`, after that there are multiple version of node which you can install (learn more about it [here](https://github.com/nvm-sh/nvm#about))
```bash
# you can use a specific version 
nvm install v12.18.3 

# to get the latest version of node (node is an alias of latest version)
nvm install node 
```
Next before using node update the `npm` and install `yarn` 
```bash 
npm i -g npm yarn
```

### Code Editors - Neovim, vscode 
I prefer `Neovim` for most of my `c++/js/php/python` projects and use `vscode` when I break neovim or when working with `jupyter notebooks`, you can install whatever you feel comfortable with

Neovim's installation and configuration is a bit tricker if you have just started using vim (When I started using vim, the autocompletion was broken `youcompleteme(ycm)` was throwing errors, `vim` wasn't able to find `python3` and so on, it took me two days to build `vim` from source and setup `ycm` still did't work so I'm using Neovim now). 

```bash 
brew install neovim
``` 

you need to have to configuration file for `nvim` there is cool trick to share the `.vimrc` for both vim and vnim, but I only use nvim. therfore create a file `touch ./config/nvim/init.vim` or place you old config file 

Install `vim-plug` - minimalistic plugin for vim ig, use whatever you like `vundle, noebundle?` that doesn't matter much.
```bash
curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
```

I am assuming you know how to configure vim, if not the case there are tons of videos on vim configuration and setup (by far my fav guy is [theprimeagen](https://www.youtube.com/c/ThePrimeagen/videos). Alright, its time for goodness, open `nvim`, ignore the errors and do `:PlugInstall`.





install coc-clangd, open nvim and do `:CocInstall coc-clangd`, and other language lsp you wish to support.


### Install LLVM, clangd (LSP for C++)
```bash
brew install llvm
```
add `bits/stdc++.h` in the include dir
inside `/usr/local/include/`
create a dir `mkdir bits` and copy the stdc++.h file here
