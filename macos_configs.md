# macOS Configuration

## System Configurations

```sh
#Disable accent press
defaults write -g ApplePressAndHoldEnabled -bool false
```

## Dock Configuration

```sh
# Remove the dock autohide delay
defaults write com.apple.dock autohide-delay -float 0
# Make hidden apps in dock appear translucent
defaults write com.apple.Dock showhidden -bool YES
killall Dock
```

## Terminal Configurations

### Homebrew Installation

```sh
# Install Homebrew
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Add Homebrew to your PATH
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> /Users/[username]/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"
```

### iTerm2 Installation

```sh
brew install --cask iterm2
```

### Oh My Zsh Installation

```sh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

_Note: Previous settings will be saved to `~/.zshrc.pre-oh-my-zsh`._

### Theme: PowerLevel10k

```sh
git clone https://github.com/romkatv/powerlevel10k.git $ZSH_CUSTOM/themes/powerlevel10k
```

_Note: Set the theme in `~/.zshrc`_

```sh
ZSH_THEME="powerlevel10k/powerlevel10k"
```

### Zsh Plugins Installation

#### zsh-autosuggestions

```sh
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

#### zsh-syntax-highlighting

```sh
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

_Note: Configure plugins in `~/.zshrc`_

```sh
plugins=(git zsh-autosuggestions zsh-syntax-highlighting web-search)
```

### Terminal Utilities

#### VSCode FindItFaster

```sh
https://github.com/tomrijndorp/vscode-finditfaster
```

#### fzf

```sh
#Install using Homebrew
brew install fzf

# Set up fzf key bindings and fuzzy completion
source <(fzf --zsh)

#Optional: Update
brew update; brew upgrade fzf
```

#### rigrep

```sh
#Install using Homebrew
brew install ripgrep
```

#### bat

```sh
#Install using Homebrew
brew install bat
```

#### tree

```sh
#Install using Homebrew
brew install tree
```

#### lsd

```sh
#Install using homebrew
brew install lsd

#Create alias
alias ls="lsd -hA --group-dirs first"
```

#### tree

```sh
#Install using homebrew
brew install tree

#Create alias
alias tree="tree -a -L 2 -h -f"
```

### Custom Functions && Oh My Zsh

\*Note: All of these are in ~/.zshrc

#### fuzzy cd

```sh
fcd() {
  local dir
  dir=$(fzf --select-1 --exit-0 --preview 'tree -C {} | head -200')
  if [[ $? -eq 0 && -n "$dir" ]]; then
    if [[ -d "$dir" ]]; then
      cd "$dir"
    else
      cd "$(dirname "$dir")"
    fi
  fi
}
```

#### fuzzy open finder

```sh
fop() {
  local file
  file=$(fzf --select-1 --exit-0 --preview 'cat {} | head -200')
  if [[ $? -ne 0 ]]; then
    return
  fi
  if [[ -n "$file" ]]; then
    local dir
    dir=$(dirname "$file")
    open -a Finder "$dir"
  fi
}
```

#### fuzzy open vscode

```sh
vsc() {
  local file
  file=$(fzf --select-1 --exit-0 --preview 'cat {} | head -200')
  if [[ $? -ne 0 ]]; then
    return
  fi
  if [[ -n "$file" ]]; then
    local dir
    dir=$(dirname "$file")
    code "$dir"
  fi
}

#Create an alias overriding code
alias code="vsc"
```

#### ip

```sh
alias ip="ipconfig getifaddr en0"
```

#### utils

```sh
alias ls="lsd -hA --group-dirs first"
alias tree="tree -a -L 4 -h -f"
alias ip="ipconfig getifaddr en0"
alias detach="tmux detach"
alias tnew='tmux new -s'
alias attach='tmux attach -t'
alias gitnuke='git clean -df && git reset HEAD --hard'
```
