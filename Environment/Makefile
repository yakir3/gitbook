MAINTAINER = yakir
APPFILES = $(CURDIR)/Appfiles
DOTFILES = $(CURDIR)/Dotfiles


UNAME := $(shell uname)
ifeq ($(UNAME), Darwin)
	INSTALL_CMD := brew install
	PACKAGE := iterm2
else ifeq ($(UNAME), Linux)
	INSTALL_CMD := sudo apt install -y
	PACKAGE := vim git svn telnet wget curl make cmake zsh
else
	$(error Unsupported operating system: $(UNAME))
endif

.PHONY: all macos ubuntu test clean
all: test clean ## test then clean

macos: homebrew install-package install-fonts vimrc zshrc ## MacOS init
	@echo "##### MacOS init start #####"
	@echo "##### MacOS init end #####"

ubuntu: install-package install-fonts vimrc zshrc ## Ubuntu init
	@echo "##### Ubuntu init start #####"
	@echo "##### Ubuntu init end #####"


test: ## Run the tests
	@echo "##### test step start #####"
	@echo $(APPFILES)
	@echo $(DOTFILES)
	@echo $(UNAME)
	@echo $(INSTALL_CMD) $(PACKAGE)
	@echo "##### test step end #####"

clean: ## Clean tmp files
	@echo "##### clean step start #####"
	rm -rf /tmp/fonts/
	@echo "##### clean step end #####"


##### tools #####
.PHONY: vimrc zshrc install-fonts install-package homebrew

vimrc:
	@echo "##### vimrc step start #####"
	# Install Vundle.vim
	git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim
	# Copy .vimrc to HOME
	cp -a $(DOTFILES)/.vimrc $(HOME)/.vimrc
	# Install all vim plugins
	vim +PluginInstall +qall 
	# Install colorshceme and set to molokai
	mkdir ~/.vim/colors && cp ~/.vim/bundle/ex-colorschemes/colors/molokai.vim ~/.vim/colors/
	@echo "##### vimrc step end #####"

BREW_BIN_PATH = $(shell dirname `which brew`)
# zshrc: install-fonts
zshrc:
	@echo "##### zshrc step start #####"
	# Change shell to zsh
	chsh -s $(shell which zsh)
	# Install oh-my-zsh and plugin
	git clone https://github.com/ohmyzsh/ohmyzsh.git ~/.oh-my-zsh
	git clone https://github.com/zsh-users/zsh-autosuggestions ~/.oh-my-zsh/custom/plugins/zsh-autosuggestions
	git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ~/.oh-my-zsh/custom/plugins/zsh-syntax-highlighting
	# Copy .zshrc to HOME
	sed -i "" "s#BREW_BIN_PATH#$(BREW_BIN_PATH)#" $(DOTFILES)/.zshrc
	cp -a $(DOTFILES)/.zshrc $(HOME)/.zshrc
	@echo "##### zshrc step end #####"

install-fonts:
	@echo "##### install-fonts step start #####"
	git clone https://github.com/powerline/fonts.git --depth=1 /tmp/fonts
	/tmp/fonts/install.sh
	@echo "##### install-fonts step start #####"

install-package:
	@echo "##### install-package step start #####"
	# Allow Mac to install software from any source	
	sudo spctl --master-disable
	$(INSTALL_CMD) $(PACKAGE)
	@echo "##### install-package step start #####"

homebrew:
	bash -c "$(shell curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

.PHONY: help
help:
	@grep -E '^[a-zA-Z_-]+:.*?## .*$$' $(MAKEFILE_LIST) | sort | awk 'BEGIN {FS = ":.*?## "}; {printf "\033[36m%-30s\033[0m %s\n", $$1, $$2}'