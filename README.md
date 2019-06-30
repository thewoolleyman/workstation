# Table of Contents

* [Overview](#overview)
* [OSX workstation](#osx-workstation)
* [Visual Studio Code Setup](#visual-studio-code-setup)
* [Jetbrains overridden settings](#jetbrains-overridden-settings)
* [Ubuntu Workstation](#ubuntu-workstation)

# Overview

These are the steps that I use to set up my development workstations.  I have used
automated tools and scripts.  I believe those are useful for shared-workstation
team environments, where you have to set up new workstations weekly or montly.
But for personal workstations, which you set up yearly or more, automation is
not worth the maintenance overhead, in my experience.

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

NOTES FOR 2019 / Mojave

* download chrome (and/or Firefox) and make default
  * Chrome Extensions
    * Chrome JSON Formatter extension https://github.com/callumlocke/json-formatter
    * Lastpass
    * ~~RIP Xmarks~~
* System Prefs - Keyboard
  * Max key repeat, shorter delay until repeat.
  * Normal Keyboard: Use function keys as standard function keys
  * Macbook Touchbar: Leave to defaults (Touch Bar shows: App Controls with Control Strip; Press Fn key to: F1, F2 keys...;
* Cmd-Shift-. (period) to show hidden files in Finder
* Install any system updates
* Install Xcode from App Store
* Install Command Line Tools: `xcode-select --install`
* install iterm, tweak prefs:
  * General -> "Characters considered part of word for selection:" -> Remove "`\`"
  * Appearance -> Dimming -> Dim background windows
  * Appearance -> Tabs: Check "Show tab bar even when there is only one tab"
  * Profiles -> Default (starred) Profile -> Keys -> Left Option acts as `Esc+`
  * Profiles -> Default -> General -> Working Directory: Select "Reuse previous session's directory"
  * Profiles -> Default -> Terminal -> Scrollback Buffer -> Scrollback lines: Check "Unlimited Scrollback"   
* set nopasswd sudoers - `sudo visudo`, change "`%admin ...`" line to read: `%admin   ALL=(ALL) NOPASSWD:ALL`
* Install Dropbox and optionally remove large folders from selective sync
* symlink in home directory configs from dropbox: .ssh, .gitconfig, .gitignore_global
* install spectacle
  * Give accessibility permissions, run on login
  * Remove all default keybindings, add back only (to prevent conflicts with Jetbrains defaults):
    * ctrl-option-cmd ("smash") arrows for top/bottom/right/left
    * smash-m for fullscreen
    * smash-n for next display
    * smash-shift-up for top right
    * smash-shift-right for bottom-right
* Install [Clipy](https://clipy-app.com/), launch on system startup. Change Prefs:
  * General -> max clipboard history size 2000
  * Menu -> inline: 30, inside folder: 30, characters in menu: 200
  * Change main shortcut Ctrl+Opt+Cmd+V, disable other shortcuts (to not conflict with Jetbrains)
* install homebrew
* brew install jq watch wget coreutils yarn pkgconfig libxml2
* `brew install openssl` then add to ~/.bash_profile: `export LIBRARY_PATH=$LIBRARY_PATH:/usr/local/opt/openssl/lib/`
  * Needed for various stuff to compile, e.g. ruby mysql2 gem.
* `brew install rbenv`
* `rbenv init` and set up hook in `~/.bash_profile` as instructed: `eval "$(rbenv init -)"`
* `rbenv install -l`, pick the one you want, e.g. `rbenv install 2.5.5`
* brew install direnv
* Review following to set appropriate rbenv defaults: https://github.com/rbenv/rbenv#environment-variables
* Add bash aliases to `~/.bash_profile`:
  * Add `alias gst='git status'` - the only alias I use ;)
* Install Jetbrains Toolbox and desired IDEs, configure using section below
* Install Slack
* Install [Choosy](https://www.choosyosx.com/), if using different browsers dedicated for different employers or personal use.
* Install Zoom
* Install Visual Studio Code and [set it up](#visual-studio-code-setup)
* Install Textmate 2
  * Preferences -> Projects -> Include Files Matching: `{*,.*}`
  * Configure autosave: add `saveOnBlur = true` to top of `~/Library/Application\ Support/TextMate/Global.tmProperties`
* Additional browsers as necessary: Canary, Firefox, Opera
* Turn off system prefs for trackpad swipe between pages because it makes you lose your duolingo lesson >:-(
* Docker
* `brew cask install java`
* Other apps
  * Kindle app (via App Store)
  * Acrobat Reader

# OSX Workstation Optional

* Haskell
  * Follow instructions on [haskell stack page](https://docs.haskellstack.org/en/stable/install_and_upgrade/#macos) (`brew install haskell-stack`)
  * Review https://lexi-lambda.github.io/blog/2018/02/10/an-opinionated-guide-to-haskell-in-2018/
* Elixir/Phoenix
  * Erlang/Elixir: `brew install elixir`
  * Hex package manager: `mix local.hex`
  * Phoenix: `mix archive.install https://github.com/phoenixframework/archives/raw/master/phoenix_new.ez`

# Visual Studio Code Setup
## Packages
* Install Intellij Keybindings: https://github.com/kasecato/vscode-intellij-idea-keybindings
* Install Purescript IDE: https://github.com/nwolverson/vscode-ide-purescript

# Jetbrains overridden settings
* Appearance & Behavior -> Appearance -> Use custom font -> change to 14
* Keymap -> Show F1, F2, etc. keys on the touch bar (checkbox at bottom).
* Editor -> Color Scheme -> Darcula
* Editor -> Color Scheme -> Ruby -> Line Continuation -> Background -> 3B3B3B
* Editor -> General -> Maximum Number of contents to keep in clipboard -> 100
* Editor -> General -> Recent files limit -> 100
* Editor -> General -> Editor Tabs -> Turn off: Show tab tooltips
* Editor -> General -> Smart Keys -> Turn off: Use "CamelHumps" words
* Editor -> General -> Smart Keys -> Turn on: Surround selection on typing quote or brace
* Editor -> General -> Smart Keys -> Ruby -> Turn on: Start ruby interpolation in strings on #
* Editor -> Code Style ->
  * Java: Set Continuation Indent to 4 (instead of default 8)
  * Javascript, Typescript -> Punctuation: 
    * Don't Use semicolon to terminate statements
    * Use single quotes always
  * Ruby: Tabs and Indents: Indent methods after access **ALL** modifiers (**only to match
    default Rails generator formatting, otherwise prefer not to because it takes more space**)
  * Ruby: Other: Spaces around curly braces in hashes **AND** blocks (**only to match
    default Rails generator formatting, otherwise prefer not to because it takes more space**)
  * HTML, Style Sheets (CSS), Javascript, Typescript, Other File Types: Set Tab size and indent to 2 and continuous (instead of default 4)
* Editor -> Inspections
  * HTML -> Deprecated HTML attribute -> Turn off (incorrectly matches React component props)
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
  * Build Tools -> Gradle
    * Use auto-import
    * Using explicit module groups
    * Use gradle 'wrapper' task configuration
    * Everything else unchecked
  * Build Tools -> Gradle -> Runner -> Delegate IDE build/run actions to gradle
  * Compiler
    * Build Project Automatically: Turn on
* Keystroke-Learning Plugins
  * Force Shortcuts
  * Key Promoter
  * Presentation Assistant
* Haskell plugin
  * Use [the one named `intellij-haskell`](https://plugins.jetbrains.com/plugin/8258-intellij-haskell), **NOT**
    the `haskell` one by jetbrains!  Note this **only works in Intellij**, not Rubymine, Webstorm, etc.
  * Follow [Getting Started instructions in the readme](https://github.com/rikvdkleij/intellij-haskell/blob/master/README.md#getting-started)  
* Idea-only settings for Elixir
  * Configure *.eex to display as RHTML (syntax is similar enough to get highlighting right)
    * Install Ruby Plugin
    * Editor -> File Types -> RHTML: Add "*.eex" as type
    * Editor -> Inspections -> Ruby -> Unresolved Ruby Reference: Uncheck
    * Editor -> Inspections -> Ruby -> Double Quoted String: Uncheck

# Ubuntu Workstation

**NOTE: This Ubuntu section is way outdated, but I kept it here for reference.
It dates back to my last attempt at going back to a Linux workstation, which I gave
up on after a week, because I can't live without the MacOS command key (it's like not
having a left thumb).**

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
  
# Chad's Printer

* 10.0.100.199
* LPD Line Printer Daemon
* HP Laserjet 4MP
