# Personal Mac Ansible Playbook

Automates mac setup with Ansible. Should be idempotent.

## Installation

1. Install apple's command line tools with `xcode-select --install`
2. Log into iCloud and Mac App Store
3. Install Ansible
   1. Run the following command to add Python 3 to your $PATH: `export PATH="$HOME/Library/Python/3.8/bin:/opt/homebrew/bin:$PATH"`
   2. Upgrade Pip: `sudo pip3 install --upgrade pip`
   3. Install Ansible: `pip3 install ansible`
4. Clone or download this repository to your local drive
5. `cd` into the folder and run `ansible-galaxy install -r requirements.yml` inside this directory to install required Ansible roles.
6. Run `ansible-playbook main.yml --ask-become-pass` inside this directory. Enter your macOS account password when prompted for the 'BECOME' password.
   > Note: If some Homebrew commands fail, you might need to agree to Xcode's license or fix some other Brew issue. Run `brew doctor` to see if this is the case.

# Post Install

For things that I haven't gotten around to figure out how to automate with Ansible

## Install dot files

1. Run `sh -c "$(curl -fsLS chezmoi.io/get)" -- init --apply andrew-chon` to install dotfiles for the first time
2. Run `chezmoi update` to pull changes from the repo and apply them

`chezmoi add ~/.<file>` to add to chezmoi  
`chezmoi edit ~/.<file>` to edit file  
`chezmoi diff` to see what changes chezmoi would make  
`chezmoi -v apply` to apply changes  
`chezmoi cd` then regular git commands to push changes to repo

# Overriding Defaults

Not everyone's development environment and preferred software configuration is the same.

You can override any of the defaults configured in `default.config.yml` by creating a `config.yml` file and setting the overrides in that file. For example, you can customize the installed packages and apps with something like:

```yaml
homebrew_installed_packages:
  - cowsay
  - git
  - go

mas_installed_apps:
  - { id: 443987910, name: "1Password" }
  - { id: 498486288, name: "Quick Resizer" }
  - { id: 557168941, name: "Tweetbot" }
  - { id: 497799835, name: "Xcode" }

npm_packages:
  - name: webpack

configure_dock: true
dockitems_remove:
  - Launchpad
  - TV
dockitems_persist:
  - name: "Sublime Text"
    path: "/Applications/Sublime Text.app/"
    pos: 5
```

Any variable can be overridden in `config.yml`; see the supporting roles' documentation for a complete list of available variables.
