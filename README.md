# IMPORTANT UPDATE!

**Most of this document is now deprecated! See the latest version here, from when I set up my latest GitLab workstation: https://gitlab.com/cwoolley-gitlab/cwoolley-gitlab/-/blob/main/gitlab-workstation-setup-notes.md**

The only part which will be kept up to date is the [Jetbrains overridden settings](#jetbrains-overridden-settings) section (TODO: Move the Jetbrains section to a separate dedicated page).

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
    * [1password](https://1password.com/downloads/mac/)
    * ~~Xmarks (RIP)~~ [Syncmarx](https://chrome.google.com/webstore/detail/syncmarx/llcdegcpeheociggfokjkkgciplhfdgg)
    * [Window Namer and Restorer](https://chrome.google.com/webstore/detail/window-namer-and-restorer/elgojbkcijgcpojlfhhmjnclgkofmiha)
      * Options: Limit window names to 16 chars (although try to use less).
* System Preferences - Keyboard
  * Max key repeat, shorter delay until repeat.
  * Normal Keyboard: Use function keys as standard function keys
  * Macbook Touchbar: Leave to defaults (Touch Bar shows: App Controls with Control Strip; Press Fn key to: F1, F2 keys...;
  * Shortcuts -> Services -> Text: Uncheck "Search man Page Index in Terminal" ([steals binding from Jetbrains](https://stackoverflow.com/a/55747595)).
* System Preferences - Trackpad
  * Point and Click -> Force Click and haptic feedback: Turn Off (always causes me to lose highlighting in my way when I'm drag-highlighing with the trackpad)
* System Preferences - Mission Control
  * Hot Corners... -> Disable all 
* Make everything show in Finder:
  * Finder -> home directory
    * Change to List view
    * In Menu-> View -> Show View Options -> Show Library Folder
  * Show hidden files in Finder: `defaults write com.apple.finder AppleShowAllFiles True; killall Finder` (Cmd-Shift-. (period) to toggle)
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
* Install [Context.co](https://contexts.co/)
  * Sidebar on bottom left
  * Search with `Ctrl-Space` and `Fn-<characters>`
* Install Zoom
* Install Visual Studio Code and [set it up](#visual-studio-code-setup)
* Install Textmate 2 (for quick plain text editing outside the context of an IDE project. Main requirement is that it opens instantly. Alternatives are [Sublime](https://www.sublimetext.com/download) or [CotEditor](https://coteditor.com/))
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
  * Ears: https://clickontyler.com/ears/
  * Kindle app (via App Store)
  * Acrobat Reader
* For any environment variables which are needed globally from launchd apps (e.g. Jetbrains IDEs), use the approach described here: http://www.dowdandassociates.com/blog/content/howto-set-an-environment-variable-in-mac-os-x-launchd-plist/
  * For example, `BROWSERSLIST_IGNORE_OLD_DATA=true`, to suppress stylelint warnings for outdated `caniuse-lite`, 
* If you work with large repos a lot, run `git config --global feature.manyFiles true`

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
* TODO: Try out https://github.com/zawys/vscode-as-git-mergetool to see if it's as good as Jetbrains `Resolve Conflicts` three-pane view.

## Config

* Settings -> Text Editor -> Files -> Auto Save: Set to `afterDelay`

## Language Setup

* Purescript: Install Purescript IDE: https://github.com/nwolverson/vscode-ide-purescript
* Haskell: Follow instructions in https://gitlab.com/thewoolleyman/haskell-project-setup



# Jetbrains overridden settings

**_IMPORTANT NOTE: Most of this document is now deprecated! See the latest version here, from when I set up my latest GitLab workstation: https://gitlab.com/cwoolley-gitlab/cwoolley-gitlab/-/blob/main/gitlab-workstation-setup-notes.md. The only part which will be kept up to date is the [Jetbrains overridden settings](#jetbrains-overridden-settings) section (TODO: Move the Jetbrains section to a separate dedicated page)._**

Notes: Many of these are project-level settings, and can be persisted by selectively committing config
under `.idea`.  Also, some may vary across different IDEs and projects.  So, these are more guidelines
and reminders to myself of where the settings live.  

Note that there are TWO places settings are persisted - at the IDE-level (in system preferences), and
at the project-level (in the `.idea` folder in the project).

Jetbrains has a built-in way to manage IDE-level settings, but not project-level settings.

See https://gitlab.com/jetbrains-ide-config/jetbrains-ide-config-gitlab for my process to manage
both IDE-level and project-level settings via version control.

* Appearance & Behavior -> Appearance
  * Theme: Darcula
  * Use custom font -> change to 14
  * (OPTIONAL) Use custom font: .SF NS Text
* Appearance & Behavior -> Menus and Toolbars
  * (OPTIONAL) Delete some things to give more room for file path on laptop screens 
    * Main Toolbar -> Main Toolbar Settings: Delete (minus button) this, things below it, and the separators.
    * Navigation Bar Toolbar (not sure how/why this is different than "Main Toolbar"???) -> Remove VCS options subgroup
* Appearance & Behavior -> UI Options -> Check the following:
  * Show tree indent guides
  * (OPTIONAL) Use smaller indents in trees (really only necessary to get more horizontal real estate when working on laptop screen)
  * Enable mnemonics in menu
  * Enable mnemonics in controls
  * Always show full path in menu header
* Appearance & Behavior -> Tool Windows -> Check the following:
  * Show Tool Window numbers 
* Appearance & Behavior -> System Settings
  * Enable: Save files if the IDE is idle for 15 seconds
* Editor -> Color Scheme -> Darcula
* Editor -> General -> Code Completion -> Insert selected suggestion by pressing space, dot, or other context-dependent keys -> Turn off (As of 2021.1 EAP makes annoying Rubymine doc annotation completion autocomplete when you are trying to type comments in spaces.  Hopefully this is fixed soon)
* Editor -> General -> Auto Import -> TypeScript/JavaScript -> Turn on: Unambiguous imports on the fly
* Editor -> General -> Smart Keys -> Ruby -> Turn on: Start ruby interpolation in strings on #
* Editor -> General -> Smart Keys -> Javascript -> Turn on: Start template string interpolation in strings on typing '$'
* Editor -> General -> Smart Keys -> YAML -> Turn OFF: Auto expand key sequences upon paste (tries to wrap lines when pasting colons in comments)
* Editor -> File Types -> Ignored Files and Folders
  * Add `*.edit.po` (translation files in GitLab, they are in `.gitignore` and thus automatically excluded in IDE anyway).
* Editor -> Font -> Size -> change to 15
* Editor -> Font -> Line height -> change to 0.9 (More density on laptop screens)
* Editor -> Code Style -> General tab:
    * Hard wrap at 100 columns (leave wrap on typing unchecked)
* Editor -> Code Style -> Formatter tab:
    * Check "Turn formatter on/off with markers in code comments" - allows disabling autoformatting if it conflicts with
      prettier/rubycop/linter settings in project, so you can still autoformat the rest of the entire file.
* Editor -> Code Style ->
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
  * Java (if it exists in current IDE): Set Continuation Indent to 2 (instead of default 8)
  * Javascript AND Typescript -> 
    * Wrapping and Braces: (needed to make "prettier" defaults happy)
      * Function call arguments:
        * Chop down if long
        * New line after '('
        * Place ')' on new line
      * Function declaration parameters:
        * Align when multiline: Uncheck
      * ES6 import/export
        * Do not wrap
    * Punctuation: 
      * Don't Use semicolon to terminate statements always (leave on for GitLab)
      * Use single quotes always
      * Trailing comma: Add when multiline
  * Markdown (need to enable markdown plugin first)
    * Wrapping and Braces
      * Turn off: Wrap on Typing, Wrap long text, Wrap text inside block quotes (enabling these will cause it to break URLs and other things that should never be wrapped)
  * Ruby: Tabs and Indents: Indent methods after access **ALL** modifiers **ONLY IF YOU WANT to match
    default Rails generator formatting, otherwise prefer not to because it takes more space**
  * Ruby: Spaces: Spaces within curly braces in hashes **AND** blocks **ONLY IF YOU WANT to match
    default Rails generator formatting, otherwise prefer not to because it takes more space**
  * HTML, Style Sheets (CSS), Javascript, Typescript, Other File Types: Set Tab size, Indent, and Continuation Indent all to 2 (instead of default 4)
* Editor -> Code Editing
  * Error Highlighting -> The 'Next Error' action goes through: All problems
* Editor -> Inspections
  * CSS -> Unused CSS selector -> Turn off (OPTIONAL, only turn off if it can't tell if a selector with a var is used in a SCSS library file)
  * HTML -> 
    * Empty Tag -> Turn off (ONLY for React, not needed vor Vue - matches root React element) - TODO: Is this still needed even for React? Check in a React app...
    * Unknown tag -> Options -> Custom HTML Tags:
      * Add 'nuxt' (for Vue apps)
      * Add 'rootDir' (for jest config)
  * Javascript -> General ->
    * ~~Unresolved Javascript variable: Uncheck (incorrectly flags some things in Vue)~~ Seems like this works better now???
    * Unused global symbol: Uncheck (incorrectly flags some things, e.g. Nuxt config) TODO: Still needed? Check in a Nuxt app...
  * Ruby -> Naming Conventions
    * Unconventional ... name: Change max length on all from 30 to 40. Terseness is not a virtue; name things appropriately and wrap lines if ya gotta.
  * (In Idea IDE only) Kotlin -> Naming Conventions -> Class naming convention: Change to `[A-Za-z][A-Za-z\d]*` (allow lowercase first letter)
  * Proofreading -> Typo -> Options -> Uncheck "Process code"
  * Security -> Link with unencrypted protocol -> "Ignored URLs": Add "http://test.host" (for Rails apps)
* Editor -> Inlay Hints
  * Code vision -> Uncheck "Code author" (can open Annotations to see authors)
* Keymap - Mac OS X 10.5+
  * **NOTE: I've decided to learn default keymaps whenever they exist.  I now only add ones that are useful but unmapped.**
  * **Tip: "Move Caret to Text Start/End" is bound to "home/end" by default.  On a Mac small/laptop keyboard,
    use is Fn+Cmd+<right|left> for "home/end"**
  * Show F1, F2, etc. keys on the touch bar (If applicable, there will be checkbox at bottom of Keymap panel)
  * Main Menu
    * Code
      * Inspect Code...: Add Ctrl+Option+Cmd+I
    * Edit
      * Copy Path/Reference...
        * Path From Repository Root: Bind to Cmd-Shift-C (replace default keybinding of this to copy absolute path)
    * Run
      * Debugging Actions
        * Resume Program: Remove "Cmd+Option+R" shortcut and leave only F9, it's inconsistent with all the others which are Function keys, and I want the F9 function key to show up on the tooltip when hovering over the button.
    * Window
      * Editor Tabs
        * Close All: Add Cmd+Option+w
  * Version Control Systems
    * Git
      * Compare with Branch: Add Ctrl+Option+Cmd+B
    * Diff & Merge
      * Compare with Local: Add Option+D
      * Compare Before with Local: Add Shift+Option+D (conflicts with Mercurial, but I don't care)
    * Show History (for all): Add Ctrl+Option+Cmd+H
* Build, Execution, Deployment
  * (Idea IDE only) Build Tools -> Gradle
    * Use auto-import
    * Using explicit module groups
    * Use gradle 'wrapper' task configuration
    * Everything else unchecked
  * (Idea IDE only) Build Tools -> Gradle -> Runner -> Delegate IDE build/run actions to gradle
  * Compiler (If exists in IDE)
    * Build Project Automatically: Turn on
  * Other (If exists in IDE)
    * Select in Project View: Add Cmd-Shift-1
* Languages & Frameworks
  * JavaScript
    * JavaScript language version: ECMAScript 6+
    * Libraries -> Add -> (NOTE: most of these require that you **close and re-open project** for them to be picked up.)
      * Node.js Core (to make 'process.env' not complain that `process` has no import) (TODO: Is this still needed?)
        * Framework Type -> "Node.js core modules"
        * put anything for name, don't add anything else
        * **close and re-open project** - this will cause IDE to automatically change it to "Node.js Core" `predefined` type.  The entry that was added to `.idea/*.iml` will disappear on restart.
     * Prettier
       * Package: put path, e.g.: `~/workspace/gitlab-development-kit/gitlab/node_modules/prettier`
       * Put extra mask in Run for Files, e.g.: `{**/*,*}.{js,ts,jsx,tsx,vue,graphql,scss}`
       * Check "On 'Reformat Code' action"
     * Code Quality Tools -> ESLint:
       * Switch to "Manual ESLint Configuration"
       * Eslint Package: Detect package and configuration file from nearest package.json
       * "Working directories": Enter a single dot `.`
       * Configuration file: Automatic Search
       * Additional rules dir: blank
       * Extra eslint options: blank
       * RUn for files: `{**/*,*}.{js,ts,jsx,tsx,html,vue}`
       * These manual settings are a workaround for this bug, which results in a red error for eslint config in JetBrains when viewing JS files: https://youtrack.jetbrains.com/issue/WEB-47385#focus=Comments-27-5119207.0-0
       * You may have to restart the IDE and/or re-save the settings a few times to make the error go away (???)
  * Markdown
    * Automatic assistance in the editor: Turn off - it prevents numbering of ordered lists with all `1.`; it forces them to be sequential. See bug: https://youtrack.jetbrains.com/issue/IDEA-292704/Do-not-automatically-number-lists-in-markdown
* Tools -> Terminal: Sometimes the RubyMine in-IDE Terminal can get confused and use the wrong interpreter/gems. I’ve found that I need `ASDF_RUBY_VERSION=2.7.7` (or whatever is in your `.tool-version`) in `Tools -> Terminal -> Environment Variables` to make it work, even if I have the right SDK set in `Languages & Frameworks -> Ruby SDK and Gems`
* Advanced Settings -> IDE section: Recent files limit -> 100
* Idea-only settings for Elixir
  * Configure *.eex to display as RHTML (syntax is similar enough to get highlighting right)
    * Install Ruby Plugin
    * Editor -> File Types -> RHTML: Add "*.eex" as type
    * Editor -> Inspections -> Ruby -> Unresolved Ruby Reference: Uncheck
    * Editor -> Inspections -> Ruby -> Double Quoted String: Uncheck
* PLUGINS: My curated list of Jetbrains plugins I use has moved to
  [the RubyMine Plugins section of my GitLab Workstation Setup Notes](https://gitlab.com/cwoolley-gitlab/cwoolley-gitlab/-/blob/main/gitlab-workstation-setup-notes.md#rubymine-plugins). Please visit that link for the latest updates.


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
