# workstation

UPDATED MANUAL NOTES FOR 2017 / Sierra

* Set function keys to work as function keys
* set nopasswd sudoers
* symlink in home directory configs: .ssh, .gitconfig, .gitignore
* download chrome and make default
* install spectacle and run on login
* install iterm
* install homebrew
* brew install chruby and ruby-install and put hooks and default ruby in `/etc/bashrc`
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

## Jetbrains overridden settings
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
