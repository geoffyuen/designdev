# Environment

Maintain installed programs and migrate your apps to a new Mac

## Use Homebrew to install utilities and applications

Install Homebrew:

`ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`

Install commandline programs like so:

`brew install node`

Uninstall:

`brew uninstall node`

Update/upgrade

`brew update` (all programs) or `brew update node`

List installed

`brew list` (includes dependencies) or `brew leaves` <- for top level

Install desktop apps

`brew cask install google-chrome`

Save installed apps to text file

`brew cask list > casks.txt`

Install apps from text file

`xargs brew install < brew.txt`

## Install Apps from the Mac App Store (MAS)

First you need the mas commandline utility:

```
brew install mas
brew tap mas-cli/tap
brew tap-pin mas-cli/tap
```

Search for an app

`mas search transmit`

Install an app

`mas install {{ id_number_from_above }}`

Some great insight here: https://hackernoon.com/personal-macos-workspace-setup-adf61869cd79
