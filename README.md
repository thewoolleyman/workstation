# OSX workstation

UPDATED MANUAL NOTES FOR 2017 / Sierra

* Set function keys to work as function keys
* set nopasswd sudoers
* symlink in home directory configs: .ssh, .gitconfig, .gitignore
* download chrome and make default
* install spectacle and run on login
* install iterm
* install homebrew
* brew install chruby and ruby-install and put hooks and default ruby in `/etc/bashrc`
* brew install jq
* Install Rubymine and Intellij
* Install Dropbox and optionally remove large folders from selective sync
* Install Slack
* Install Zoom
* Install Atom
* Install Flycut
  * Launch on login, remove duplicated, change icon to scissors
  * Change shortcut Ctrl+Opt+Cmd+V to not conflict with Jetbrains
* Additional browsers as necessary: Canary, Firefox, Opera
* Turn off system prefs for trackpad swipe between pages because it makes you lose your duolingo lesson >:-(
* Docker
* Elixir/Phoenix
  * Erlang/Elixir: `brew install elixir`
  * Hex package manager: `mix local.hex`
  * Phoenix: `mix archive.install https://github.com/phoenixframework/archives/raw/master/phoenix_new.ez`

# Ubuntu Workstation

MANUAL NOTES FOR Ubuntu 17.04

Not everything is listed, main things and gotchas mostly

NOTE: Installed packages from command line, manually fixing any dependencies needed.

* System Settings
  * Mouse and Touchpad
    * Turn off tap to click
  * Brightness and Lock
    * Turn off lock
  * Keyboard -> Shortcuts -> Launchers -> Key to show the HUD: Backspace to disable
* Fix keyring issue
  * https://askubuntu.com/a/735463
* Files - Preferences
  * Allow Folders to be Expanded
* Install Chrome
  * Set as default browser
  * Log in to google account in prefs
    * Advanced Sync: Disable for bookmarks, passwords, open tabs, and credit cards
  * Choose where to save files
  * Always show bookmarks bar
* Install Dropbox
  * Install according to official instructions
  * Fix bug with toolbar menu not rendering: http://www.webupd8.org/2016/06/fix-dropbox-indicator-icon-and-menu-not.html
  * Bug still not fixed, uninstall `dropbox` via `apt`, then reinstall `nautilus-dropbox` and it works.
* Symlink in `~/.ssh` from Dropbox
* Intellij and rubymine
  * download, untar, run `bin/idea.sh` and `bin/mine.sh`
* Atom
* Apt packages:
  * `sudo apt install git emacs`
* Crashplan
* Spacemacs
  * After install, symlink `~/.spacemacs` from Dropbox.
* Slack
* chruby and ruby-install and put hooks and default ruby in `/etc/bashrc`
* Elixir/Phoenix
  * Erlang/Elixir: follow instructions on elixir webpage
  * Hex package manager: `mix local.hex`
  * Phoenix: `mix archive.install https://github.com/phoenixframework/archives/raw/master/phoenix_new.ez`
  

# Jetbrains overridden settings
* Keybindings
  * Editor Actions
    * Choose Lookup Item Replace: Add Enter binding (confirm to remove from several other places)
    * Enter: Remove Enter binding (leave unbound)
    * Move Caret to Text End: Add Cmd+Down Arrow binding
    * Move Caret to Text Start: Add Cmd+Up Arrow binding
    * Next Template Variable or Finish In-Place Refactoring: Remove Enter binding (leave only Tab)
  * Main Menu
    * View
      * Jump To Source: Remove Cmd+Down Arrow binding
    * Navigate
      * Related Data: Add F4 Binding
      * Jump to Navigation Bar: Remove Cmd+Up Arrow
  * Version Control Systems
    * Show History (for all): Add Ctrl+Option+Cmd+H
  * Database Tools and SQL
    * Edit: Remove Enter
  * Other
    * Various removals of Enter
