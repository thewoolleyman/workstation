# Table of Contents

* [Overview](#overview)
* [OSX workstation](#osx-workstation)
* [Visual Studio Code Setup](#visual-studio-code-setup)
* [Jetbrains overridden settings](#jetbrains-overridden-settings)
* [Ubuntu Workstation](#ubuntu-workstation)
* [Printers](#printers)

# Overview

These are the steps that I use to set up my development workstations.  I have used
automated tools and scripts.  I believe those are useful for shared-workstation
team environments, where you have to set up new workstations weekly or monthly.
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

NOTES FOR 2020 / Catalina

* download chrome (and/or Firefox) and make default
  * Chrome Extensions
    * Chrome JSON Formatter extension https://github.com/callumlocke/json-formatter
    * ~~Lastpass~~ [1password](https://1password.com/downloads/mac/)
    * ~~Xmarks (RIP)~~ [Syncmarx](https://chrome.google.com/webstore/detail/syncmarx/llcdegcpeheociggfokjkkgciplhfdgg)
* System Preferences - Keyboard
  * Max key repeat, shorter delay until repeat.
  * Normal Keyboard: Use function keys as standard function keys
  * Macbook Touchbar: Leave to defaults (Touch Bar shows: App Controls with Control Strip; Press Fn key to: F1, F2 keys...;
  * Shortcuts -> Services -> Text: Uncheck "Search man Page Index in Terminal" ([steals binding from Jetbrains](https://stackoverflow.com/a/55747595)).
* System Preferences - Trackpad
  * Point and Click -> Force Click and haptic feedback: Turn Off (always causes me to lose highlighting in my way when I'm drag-highlighing with the trackpad)
* Make everything show in Finder:
  * Finder -> home directory
    * Change to List view
    * In Menu-> View -> Show View Options -> Show Library Folder
  * Cmd-Shift-. (period) to show hidden files in Finder (TODO: How to make this permanent?)
* Install any system updates
* Install Xcode from App Store
* Install Command Line Tools: `xcode-select --install`
* install iterm, tweak prefs:
  * (macbooks): In MacOS 'iTerm2' menu under 'Customize Touch Bar', drag off things next to escape key so you don't accidentally hit it.
  * General -> Selection -> "Characters considered part of word for selection:" -> Remove "`\`"
  * Appearance -> Tabs: Check "Show tab bar even when there is only one tab"
  * Appearance -> Dimming -> Dim background windows
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
* Follow [instructions here](https://github.com/nijicha/install_nodejs_and_yarn_homebrew) to install NVM, NodeJS, and yarn.  Important part is that node is installed and managed via ~~NVM~~ asdf, not homebrew, so you need to "fool" homebrew into using the asdf~~NVM~~-managed version of node as a dependency. **This didn't work right with asdf.**
* `brew install jq watch wget coreutils kgconfig libxml2`
* `brew install openssl` then add to `~/.zshrc`: `export LIBRARY_PATH=$LIBRARY_PATH:/usr/local/opt/openssl/lib/`
  * Needed for various stuff to compile, e.g. ruby mysql2 gem.
* `brew install rbenv` then add to `~/.zshrc` the export RUBY_CONFIGURE_OPTS line from the printout
* `rbenv init` and set up hook in `~/.zshrc` as instructed: `eval "$(rbenv init -)"`
* `rbenv install -l`, pick the one you want, e.g. `rbenv install 2.5.5`
* `brew install direnv`
* If needed, review following to set appropriate rbenv defaults: https://github.com/rbenv/rbenv#environment-variables
* Add bash aliases to `~/.zshrc`:
  * Add `alias gst='git status'`
* Add git config aliases:
  * `$ git config --global alias.ci commit`
  * `$ git config --global alias.co checkout`
  * `$ git config --global alias.sw switch`  
* For multiple users on the same computer
  * [link to slack exchange post](https://apple.stackexchange.com/questions/1393/are-my-permissions-for-usr-local-correct/189404#189404)
  * `sudo chgrp -R admin /usr/local /Library/Caches/Homebrew`
  * `sudo chmod -R g+w /usr/local /Library/Caches/Homebrew`
* Install Jetbrains Toolbox and desired IDEs, configure using section below
* Install Slack
* Install [Choosy](https://www.choosyosx.com/), if using different browsers dedicated for different employers or personal use.
* Install Zoom
* Install Visual Studio Code and [set it up](#visual-studio-code-setup)
* Install Textmate 2
  * Preferences -> Projects -> Include Files Matching: `{*,.*}`
  * Preferences -> Terminal _> Install Shell support
  * Configure autosave: add `saveOnBlur = true` to top of `~/Library/Application\ Support/TextMate/Global.tmProperties`
* Additional browsers as necessary: Canary, Firefox, Opera
* Turn off system prefs for trackpad swipe between pages because it makes you lose your duolingo lesson >:-(
* Docker
* `brew cask install java`
* [`git-together`](https://github.com/kejadlen/git-together)
  * `brew install pivotal/tap/git-together`
  * `echo 'alias git=git-together' >> ~/.bash_profile`
  * `git config --global git-together.aliases ci`
* [PyEnv Python installation steps to get the latest tcl/tk version](https://github.com/pyenv/pyenv/issues/1375#issuecomment-524280004)
* Other apps
  * Kindle app (via App Store)
  * Acrobat Reader
* For any environment variables which are needed globally from launchd apps (e.g. Jetbrains IDEs), use the approach described here: http://www.dowdandassociates.com/blog/content/howto-set-an-environment-variable-in-mac-os-x-launchd-plist/
  * For example, `BROWSERSLIST_IGNORE_OLD_DATA=true`, to suppress stylelint warnings for outdated `caniuse-lite`, 

# OSX Workstation Optional

* Haskell
  * Follow instructions in https://gitlab.com/thewoolleyman/haskell-project-setup
    * Make sure to review https://lexi-lambda.github.io/blog/2018/02/10/an-opinionated-guide-to-haskell-in-2018/ and other links in that repo.
* Elixir/Phoenix
  * Erlang/Elixir: `brew install elixir`
  * Hex package manager: `mix local.hex`
  * Phoenix: `mix archive.install https://github.com/phoenixframework/archives/raw/master/phoenix_new.ez`

# Visual Studio Code Setup

## Packages

* Install Intellij Keybindings: https://github.com/kasecato/vscode-intellij-idea-keybindings

## Config

* Settings -> Text Editor -> Files -> Auto Save: Set to `afterDelay`

## Language Setup

* Purescript: Install Purescript IDE: https://github.com/nwolverson/vscode-ide-purescript
* Haskell: Follow instructions in https://gitlab.com/thewoolleyman/haskell-project-setup

# Jetbrains overridden settings

Notes: Many of these are project-level settings, and can be persisted by selectively committing config
under `.idea`.  Also, some may vary across different IDEs and projects.  So, these are more guidelines
and reminders to myself of where the settings live.  ~~See also https://github.com/pivotal-legacy/pivotal_ide_prefs
for IDE-level settings (i.e., not project-level ones that live under `.idea`).~~

* Appearance & Behavior -> Appearance
  * Theme: Darcula, check "Use dark window headers"
  * Use custom font -> change to 14
* Editor -> Color Scheme -> Darcula
* ~~Editor -> Color Scheme -> Ruby -> Line Continuation -> Background -> 3B3B3B~~ (it's now a more sane 272727)
* ~~Editor -> General -> Maximum Number of contents to keep in clipboard -> 100~~ (this doesn't exist anymore?)
* Editor -> General -> Limits section: Recent files limit -> 100
* ~~Editor -> General -> Editor Tabs -> Turn off: Show tab tooltips~~ (this doesn't exist anymore?)
* Editor -> General -> Auto Import -> TypeScript/JavaScript -> Turn on: Unambiguous imports on the fly
* ~~Editor -> General -> Smart Keys -> Turn off: Use "CamelHumps" words~~ (now the default)
* ~~Editor -> General -> Smart Keys -> Turn on: Surround selection on typing quote or brace~~ (now the default)
* Editor -> General -> Smart Keys -> Ruby -> Turn on: Start ruby interpolation in strings on #
* Editor -> General -> Smart Keys -> Javascript -> Turn on: Start template string interpolation in strings on typing '$'
* Editor -> Font -> Size -> change to 14
* Editor -> Font -> Line spacing -> change to 0.9 (More density on laptop screens)
* Editor -> Code Style ->
  * General: Hard wrap at 80 columns
  * HTML: 
    * Other:
      * Spaces:
        * Check "In empty tag" (compatibility with default 'prettier' config)
      * Do not indent children of: -> add "script" and "style" (for compatibility with default 'prettier' formatting)
    * Arrangement
      * These are particularly tricky to get right. I attempt to get them to match
        https://vuejs.org/v2/style-guide/#Element-attribute-order-recommended, but the
        source of truth is just running eslint with `vue/attributes-order`.  See the `.idea`
        folder checked into one of my recent Vue open source repos for details.
  * Java: Set Continuation Indent to 2 (instead of default 8)
  * Javascript, Typescript -> 
    * Wrapping and Braces: (needed to make "prettier" defaults happy)
      * Function call arguments:
        * Chop down if long
        * New line after '('
        * Place ')' on new line
      * ES6 import/export
        * Do not wrap
    * Punctuation: 
      * Don't Use semicolon to terminate statements always
      * Use single quotes always
      * Trailing comma: Add when multiline
    * Imports:
      * ~~Sort imports by modules: Uncheck (conflicts with default Vue 'import/order')~~ (now the default)
  * Ruby: Tabs and Indents: Indent methods after access **ALL** modifiers (**only to match
    default Rails generator formatting, otherwise prefer not to because it takes more space**)
  * Ruby: Other: Spaces around curly braces in hashes **AND** blocks (**only to match
    default Rails generator formatting, otherwise prefer not to because it takes more space**)
  * HTML, Style Sheets (CSS), Javascript, Typescript, Other File Types: Set Tab size, Indent, and Continuation Indent all to 2 (instead of default 4)
* Editor -> Inspections
  * CSS -> Unused CSS selector -> Turn off (can't tell if a selector with a var is used in a SCSS library file)
  * HTML -> 
    * Deprecated HTML attribute -> Turn off (incorrectly matches React component props)
    * Empty Tag -> Turn off (matches root React element)
    * File reference problems -> Turn off (incorrectly shows errors in React HTML variables) (Not in some/latest IDE versions - i.e. latest webstorm?)
    * Unknown HTML tag -> Options -> Custom HTML Tags:
      * Add 'nuxt' (for Vue apps)
      * Add 'rootDir' (for jest config)
  * Javascript -> General ->
    * Unresolved Javascript variable: Uncheck (incorrectly flags some things in Vue)
    * Unused global symbol (incorrectly flags some things, e.g. Nuxt config)
  * Kotlin -> Naming Conventions -> Class naming convention: Change to `[A-Za-z][A-Za-z\d]*` (allow lowercase first letter)
  * Proofreading -> Typo -> Options -> Uncheck "Process code"
* Keymap - Mac OS X 10.5+
  * **NOTE: I've decided to learn default keymaps whenever they exist.  I now only add ones that are useful but unmapped.**
  * **Tip: "Move Caret to Text Start/End" is bound to "home/end" by default.  On a Mac small/laptop keyboard,
    use is Fn+Cmd+<right|left> for "home/end"**
  * Show F1, F2, etc. keys on the touch bar (checkbox at bottom of Keymap panel - may not be on all/latest IDEs?).
  * Main Menu
    * Code
      * Inspect Code...: Add Ctrl+Option+Cmd+I
    * Window
      * Editor Tabs
        * Close All: Add Cmd+Option+w binding
  * Version Control Systems
    * Git
      * Compare with Branch: Add Ctrl+Option+Cmd+B
    * Diff & Merge
      * Compare with Local: Add Option+D
      * Compare Before with Local: Add Shift+Option+D (conflicts with Mercurial, but I don't care)
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
  * Other
    * Select in Project View: Add Cmd-Shift-1
* Languages & Frameworks
  * JavaScript
    * JavaScript language version: React JSX
    * Libraries -> Add -> (NOTE: most of these require that you **close and re-open project** for them to be picked up.)
      * Node.js Core (to make 'process.env' not complain that `process` has no import)
        * Framework Type -> "Node.js core modules"
        * put anything for name, don't add anything else
        * **close and re-open project** - this will cause IDE to automatically change it to "Node.js Core" `predefined` type.  The entry that was added to `.idea/*.iml` will disappear on restart.
* Misc Plugins
  * [Lines Sorter](https://plugins.jetbrains.com/plugin/5919-lines-sorter/)
  * ~~Bash Support~~ (replaced with built-in Jetbrains "Shell Script" plugin)
* Keystroke-Learning Plugins
  * Force Shortcuts (if you are hardcore and want to be forced to use keyboard)
  * Key Promoter X (if you want to be always reminded to use keyboard)
  * Presentation Assistant (if you are pair programming, and want other people to see what keystrokes you are using)
* Fun Plugins
  * Nyan Progress Bar
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

# Printers

## Chad's Printer

* 10.0.100.199
* HP Jetdirect - Socket
* HP LaserJet Series PCL 4/5

## Kristin's Printer

* HP ENVY 7643
