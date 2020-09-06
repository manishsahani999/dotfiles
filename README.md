# Hades
Tooling is hard! and necessary. This is the way I like my system to be configured. 

### Compilers, Language support and MacOS SDK 
The Xcode Command Line Tools Package is a small self-contained package available for download separately from Xcode and that allows us to do command line development in macOS. 

It consists of the macOS SDK and command-line tools, which are installed in the `/Library/Developer/CommandLineTools`.
```bash 
xcode-select --install
```

### MacOS Package Manager 
[brew](https://brew.sh/) - The Missing Package Manager for macOS.
```bash 
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```

### Install NVM, Nodejs, NPM and Yarn
```bash 
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.3/install.sh | bash
```
```bash
# you can use stable also 
nvm install v12.18.3 
```

```bash 
npm i -g npm
```

```bash 
npm i -g yarn
```

### Install LLVM, clangd (LSP for C++)
```bash
brew install llvm
```
add `bits/stdc++.h` in the include dir
inside `/usr/local/include/`
create a dir `mkdir bits` and copy the stdc++.h file here

### Install neovim 

```bash 
brew install neovim
``` 
create `./config/nvim/init.vim`

install plug 
```bash
curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
```

time for goodness, open `nvim`, ignore the errors and do `:PlugInstall`

install coc-clangd, open nvim and do `:CocInstall coc-clangd`, and other language lsp you wish to support.
