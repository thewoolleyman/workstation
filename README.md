# Overview

These are the steps that I use to set up my development workstations.  I have used
automated tools and scripts.  I believe those are useful for shared-workstation
team environments, but for personal workstations they are not worth the maintenance
overhead, in my experience.

Instead, for my personal workstations, I try to have the philosophy of
"just learn to use the defaults, unless they are missing or inconvenient".
I'll also symlink some config files/dirs into Dropbox, but on a selective
basis. 

So, what follows are some of the things I tend to install and tweak on my personal
workstations.  I've installed many other things related to the project du jour
which aren't documented here, but I've tried to remember to keep track of
most of the various little tweaks which I can never remember later.

This helps me, hopefully it helps you!

# OSX workstation

NOTES FOR 2017 / Sierra

* Set function keys to work as function keys
* set nopasswd sudoers
* symlink in home directory configs: .ssh, .gitconfig, .gitignore
* download chrome and make default
  * Chrome Extensions
    * Chrome JSON Formatter extension https://github.com/callumlocke/json-formatter
    * Lastpass
    * Xmarks
* install spectacle and run on login
* install iterm
  * Preferences -> Appearance -> Dimming -> Dim background windows
  * Preferences -> Profiles -> Default (starred) Profile -> Keys -> Left Option acts as `+Esc`
* install homebrew
* brew install jq
* brew install watch
* brew install wget
* brew install chruby and ruby-install and put hooks and default ruby in `/etc/bashrc`
* Install Rubymine and Intellij
* Install Dropbox and optionally remove large folders from selective sync
* Install Slack
* Install [Choosy](https://www.choosyosx.com/), if using different browsers dedicated for different employers vs. personal use.
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

NOTES FOR Ubuntu 17.04

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
  * `sudo apt install git emacs indicator-multiload`
  * Configure `indicator-multiload`
* Packages via Ubuntu Installer GUI
  * `okular` reader app - check support for epub before install
* Crashplan
* Spacemacs
  * After install, symlink `~/.spacemacs` from Dropbox.
* Slack
* chruby and ruby-install and put hooks and default ruby in `/etc/bashrc`
* Elixir/Phoenix
  * Erlang/Elixir: follow instructions on elixir webpage
  * Hex package manager: `mix local.hex`
  * Phoenix: `mix archive.install https://github.com/phoenixframework/archives/raw/master/phoenix_new.ez`
* golang
  * Follow instructions here: https://stackoverflow.com/a/40129734/25192
  * Install Gogland
  * Export a copy of "MacOSX 10.5+" Keymap from Idea and import
    to Gogland (until https://youtrack.jetbrains.com/issue/GO-4139 is fixed)
  
# Atom Setup
## Packages
* `sync-settings`
  * Make gist and personal access key specific to ubuntu
* `language-elixir`
* `elixir-autocomplete`

# Jetbrains overridden settings
* Editor -> General -> Maximum Number of contents to keep in clipboard -> 100
* Editor -> General -> Recent files limit -> 100
* Editor -> General -> Editor Tabs -> Turn off: Show tab tooltips
* Editor -> General -> Smart Keys -> Turn off: Use "CamelHumps" words
* Editor -> General -> Smart Keys -> Turn on: Surround selection on typing quote or brace
* Editor -> General -> Smart Keys -> Ruby -> Turn on: Start ruby interpolation in strings on #
* Editor -> Code Style ->
  * Java: Set Continuation Indent to 4 (instead of default 8)
  * Other File Types: Set Tab size and indent to 2 (instead of default 4)
* Editor -> Inspections
  * Kotlin -> Naming Conventions -> Class naming convention: Change to `[A-Za-z][A-Za-z\d]*` (allow lowercase first letter)
* Keymap - Mac OS X 10.5+
  * **NOTE: I've decided to learn default keymaps whenever they exist.  I now only add ones that are useful but unmapped.**
  * **Tip: "Move Caret to Text Start/End" is bound to "home/end" by default.  On a Mac small/laptop keyboard,
    use is Fn+Cmd+<right|left> for "home/end"**
  * Main Menu
    * Navigate
      * ~~Related Data: Add F4 Binding~~ (TODO: Document which IDE needed this and why, or delete - Idea doesn't need it)
    * Window
      * Editor Tabs
        * Close All: Add Cmd+Option+w binding
  * Version Control Systems
    * Git
      * Compare with Branch: Add Ctrl+Option+Cmd+B
    * Show History (for all): Add Ctrl+Option+Cmd+H
* Build, Execution, Deployment
  * Prefs -> Build Execution Deployment -> Build Tools -> Gradle -> Runner -> Delegate IDE build/run actions to gradle
  * Compiler
    * Build Project Automatically: Turn on
* Idea-only settings for Elixir
  * Configure *.eex to display as RHTML (syntax is similar enough to get highlighting right)
    * Install Ruby Plugin
    * Editor -> File Types -> RHTML: Add "*.eex" as type
    * Editor -> Inspections -> Ruby -> Unresolved Ruby Reference: Uncheck
    * Editor -> Inspections -> Ruby -> Double Quoted String: Uncheck
