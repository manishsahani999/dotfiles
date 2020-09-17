# Tooling is hard! and necessary

This repository presents collection of configuration setup tips and tricks. This article mainly applies to MacOS based systems and if anyone is interested contributing they are most welcome or if want to talk, they can reach me at [rec.manish.sahani@gmail.com](mailto:rec.manish.sahani@gmail.com) 

The flow of this article goes like this 
- Language Support - Compiler and Interpreters 
- System Package Manger 
- Specific Libraries and tools 
- Code Editors Configuration 
- Language Server Protocol

### Language support - Compilers and Interpreters
The first thing in the setup for any type of software development should be getting the language support - installating the compiler, interpreters etc. If you are on MacOS, the easiest way is to download and install `Xcode or Xcode Command Line`. 

I prefer Xcode Command line tools because it is compact(~1GB) and `vim` or `vscode` are enough for most of my work. But if you need a fully featured IDE and other features go ahead with Xcode(~8-10GB).

`Xcode` can be easily installed form App Store, and for `Xcode command line tools` the installation is also simple, just run the following command in terminal
```bash 
xcode-select --install
```

To verify the installation run `xcode-select -p`, this outputs the installation directory (`/Library/Developer/CommandLineTools`),

### System Package Manger - Homebrew
The installation of libraries and apps should be simple and automated, [Homebrew - The Missing Package Manager for MacOS](https://brew.sh/) is one popular package manager, the installation is just one command but requires `xcode-select` to be pre-installed (see more at [brew.sh](https://brew.sh/)).

```bash 
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```

### Specific Libraries, Tools and other Binaries  
Although `xcode-select` will provide you most of the libraries and language support, but it maybe the case that it didn't come with the lanugage of your liking (for example Nodejs).

#### JS support - NVM, Nodejs, NPM and Yarn
Js is heavily used nowdays, and `nodejs` is the most popular JS runtime. if you are working on a js based project you may need to shift between different version of node which is easily managed by [nvm](https://github.com/nvm-sh/nvm#about). It stands for node version manager, and works with any POSIX-compilant shell(bash, zsh). To install or update nvm, you should run the install script (Get the latest script from [here](https://github.com/nvm-sh/nvm#about)). 

Following is the cURL command to download and run the install script.

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

Next before using node update the `npm` and install `yarn` globally, these are most used node package manager
```bash 
npm i -g npm yarn
```

#### PHP support - Composer and extensions (Don't hate Me)
PHP is easy to learn and can be picked in two or three days, and the heavily used in web server programming. PHP comes with in `xcode-select` but there are extensions that are not supported in the pre-build MacOS PHP like `ext-gd` 

You can upgrade to PHP 7.4 using brew and replace the pre-installed MacOS version by
```bah
brew install php
```
To enable an dynamic extension just open the `php.ini` file (present at `/usr/local/etc/php/7.x/`) and uncomment the line with modules's name ex `extension=modulename` 

Composer is the PHP's dependency manager and can be installed using the following commands [see getcomposer](https://getcomposer.org/download/) for more info
```bash 
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
php -r "if (hash_file('sha384', 'composer-setup.php') === '8a6138e2a05a8c28539c9f0fb361159823655d7ad2deecb371b04a83966c61223adc522b0189079e3e9e277cd72b8897') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
php composer-setup.php
php -r "unlink('composer-setup.php');"
```
If you need help with anything related to PHP laravel development you can always ping me, I'd be happy to help.

### Code Editors - Neovim, vscode 
I prefer `Neovim` for most of my `c++/js/php/python` projects and use `vscode` when I break my neovim's configuration or when working with `jupyter notebooks`, you can install whatever you feel comfortable with, there are tons of code editors out there 

#### Vscode 
Vscode Installation is simpler, using `brew casks`, this will install vscode and add it in your path by default. 
```bash
brew cask install visual-studio-code
```

#### Neovim
Neovim's installation and configuration is a bit tricker if you have just started using vim (When I started using vim, the autocompletion was broken `youcompleteme(ycm)` was throwing errors, `vim` wasn't able to find `python3` and so on, it took me two days to build `vim` from source and setup `ycm` still did't work but that helped me found some very cool things). 

Get the latest neovim using brew by running 
```bash 
brew install neovim
``` 

you need to have to configuration file for `nvim` there is cool trick to share the `.vimrc` for both vim and vnim (google it), but I only use nvim. So for neovim create a file `touch ./config/nvim/init.vim` and edit configurations of your choice or place your old config file there  

Vim/Neovim can have extensions that are managed by `vim-plug/vundle/neobundle?`. Install the plugin that you are familiar with or go with `vim-plug` - minimalistic plugin for vim ig, use whatever you like that doesn't matter much.
```bash
# Installation of vim-plug
curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
```

I am assuming you know how to configure vim, if not the case there are tons of videos on vim configuration and setup (by far my fav guy is [theprimeagen](https://www.youtube.com/c/ThePrimeagen/videos). Alright, its time for goodness, open `nvim`, ignore the errors and do `:PlugInstall`.

Install intellisense or autocomplete for languages you used ex - for c/c++ install `coc-clangd` by  doing `:CocInstall coc-clangd` from Normal mode in vim/nvim.

### LSP 
LSP are Language Server Protocol - one configuration for all development tools. below is the image taken from [visual studio's doc](https://code.visualstudio.com/api/language-extensions/language-server-extension-guide), this gives and gist about what we are trying to achive. 
![image](https://code.visualstudio.com/assets/api/language-extensions/language-server-extension-guide/lsp-languages-editors.png)

Intellisense needs LSP for working and if its still not present in your system you may want to install it for the more productivity. 

#### LSP for C++ - LLVM, clangd
Clangd understands your C++ code and adds smart features to your editor: code completion, compile errors, go-to-definition and more. 

clangd is part of the llvm project so we need to install llvm first, that can be again installed using brew 

```bash
brew install llvm
```

After this verify that clangd is in the path using `clangd --version`


### Development Tools 

This section changes with your requirement and you may want to install apps that you are familar with or those that you use regularly. Following are tools that I use 

- **Postman** -- for API testing 
- **DBnign** -- easier for DB management

Installation is again done using brew casks
```bash 
brew cask install postman dbngin
```


### C++ Libs 
Other really important thing I like to do is add `bits/stdc++.h` in the include dir, MacOS doesn't have this header by default, never use it inside c++ projects but if you are doing any c++ coding competition its good to have it.

```bash 
# inside /usr/local/include/
cd /usr/local/include/

# create a dir bits and copy the stdc++.h file here
mkdir bits 
```
