# Personal Mac Ansible Playbook

Automates mac setup with Ansible. Should be idempotent.

## Installation
1. Go through initial setup, don't log into iCloud from setup.
2. Log into iCloud and Mac App Store once at the desktop.  Air drop 1Password link to macbook for easier login.
3. Install apple's command line tools with `xcode-select --install`
4. Install Ansible
   1. Run the following command to add Python 3 to your $PATH: `export PATH="$HOME/Library/Python/3.9/bin:/opt/homebrew/bin:$PATH"`
   2. Upgrade Pip: `sudo pip3 install --upgrade pip`
   3. Install Ansible: `pip3 install ansible`
5. Clone or download this repository to your local drive
6. `cd` into the folder and run `ansible-galaxy install -r requirements.yml` inside this directory to install required Ansible roles.
7. Run `ansible-playbook main.yml --ask-become-pass` inside this directory. Enter your macOS account password when prompted for the 'BECOME' password.
   > Note: If some Homebrew commands fail, you might need to agree to Xcode's license or fix some other Brew issue. Run `brew doctor` to see if this is the case.
8. Restart mac for system setting changes to take effect.
## Post Install

For things that I haven't gotten around to figure out how to automate with Ansible

### Install dot files

1. Run `chezmoi init git@github.com/andrew-chon/dotfiles.git` to install dotfiles for the first time
2. Run `chezmoi update` to pull changes from the repo and apply them

`chezmoi add ~/.<file>` to add to chezmoi  
`chezmoi edit ~/.<file>` to edit file  
`chezmoi diff` to see what changes chezmoi would make  
`chezmoi -v apply` to apply changes  
`chezmoi cd` then regular git commands to push changes to repo

### Setup oh my zsh

- Install oh my zsh plugins into `.oh-my-zsh/custom/plugins`
  - zsh-autosuggestions
    - done with homebrew
  - fast-syntax-highlighting
    - `git clone https://github.com/zdharma-continuum/fast-syntax-highlighting.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/plugins/fast-syntax-highlighting`
  - zsh-autocomplete
    - `git clone --depth 1 -- https://github.com/marlonrichert/zsh-autocomplete.git $ZSH_CUSTOM/plugins/zsh-autocomplete`

### Set up 1Password
- Go to settings -> developer -> set up ssh agent

### Apps to uninstall

- Freeform
- Podcasts
- Music
- Photobooth
- TV
- News
- Stocks
