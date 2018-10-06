# Web Development Tools

<!-- TOC depthFrom:2 depthTo:3 orderedList:false updateOnSave:true withLinks:true -->

- [Command-Line Tools](#command-line-tools)
  - [Important Info](#important-info)
  - [iTerm](#iterm)
  - [Hyper](#hyper)
  - [ZSH](#zsh)
  - [Oh-My-ZSH](#oh-my-zsh)
  - [z](#z)
- [Homebrew](#homebrew)
  - [Installing Homebrew](#installing-homebrew)
  - [Recommended Formulas](#recommended-formulas)
  - [Recommended Casks](#recommended-casks)
- [Node.js and npm](#nodejs-and-npm)
  - [Installing/managing Node.js via nvm](#installingmanaging-nodejs-via-nvm)
  - [Node Package Manager (npm)](#node-package-manager-npm)
  - [Global Packages](#global-packages)
- [Sass](#sass)
  - [Installing Sass](#installing-sass)
- [Composer](#composer)
- [PHP_CodeSniffer and WordPress Coding Standards (with VS Code)](#php_codesniffer-and-wordpress-coding-standards-with-vs-code)
  - [Global Install (system-wide)](#global-install-system-wide)
  - [Local Install (project-by-project basis)](#local-install-project-by-project-basis)
- [VS Code](#vs-code)
  - [Packages](#packages)
  - [Themes](#themes)
  - [Icons](#icons)
- [SSH](#ssh)
  - [Generating a new SSH key](#generating-a-new-ssh-key)
  - [Adding your SSH key to the ssh-agent](#adding-your-ssh-key-to-the-ssh-agent)
  - [SSH config file](#ssh-config-file)
  - [Some ssh-add tricks](#some-ssh-add-tricks)

<!-- /TOC -->

## Command-Line Tools

### Important Info

#### System Path

The file which lists all of the paths in your system $PATH can be found at
`/private/etc/paths`.

_Note: Not all paths will be in this file as they can also be added via the
`.zshrc` or `.bashrc` config files. You can see the full list of paths by typing
`echo $PATH` into your terminal._

#### Shell Path

The file which lists all the paths available for a terminal shell can be found
at `/private/etc/shells`.

_Note: You can see the path to the currently active shell by typing `echo $SHELL` into your terminal._

### iTerm

iTerm is a replacement for macOS's default Terminal. Download and install the
latest version of [iTerm][iterm].

### Hyper

Hyper is a replacement for macOS's default Terminal. Download and install the
latest version of [Hyper][hyper].

_Note: The Hyper config file is stored a- `/Users/paul/.hyper.js`._

#### Hyper Plugins

To enable a plugin, open your `.hyper.js` file and scroll down until you see the
spot where active plugins are defined. Once you add in the plugin you want to
install, save the file and Hyper will install it for you in the background.

```
plugins: [
  'hyper-blink',
  'hyperlinks',
  'hyper-tab-icons',
  'hyper-material-theme'
],
```

_Note: Hyper plugins are stored a- `/Users/paul/.hyper_plugins/node_modules`._

#### Recommended Hyper Plugins

- hyperline
- hyper-blink
- hyperlinks
- hyper-tab-icons
- hyper-material-theme
- hyperterm-1password

### ZSH

ZSH is a popular alternative to the Bash shell. ZSH is installed on macOS by
default but you may wish to install the most up to date version, you can do this
using Homebrew.

```
brew install zsh zsh-completions
```

Once you've installed ZSH you then need to make this version of ZSH the default
shell for your system.

Instructions for installing and setting ZSH as the default shell can be found on
the [Oh-MY-ZSH GitHub][zsh] page.

### Oh-My-ZSH

Oh-My-Zsh is a framework for managing your ZSH (Z shell) configuration. Download
and install the latest version of [Oh-My-ZSH][oh-my-zsh].

_Note: Oh-My-ZSH can be updated by running - `upgrade_oh_my_zsh`._

_Note: The Oh-My-ZSH config file is stored a- `/Users/paul/.zshrc`._

#### Oh-My-ZSH Plugins

Oh-My-ZSH comes with pre-installed [bundled plugins][oh-my-zsh-plugins]. To
enable a plugin, open your `.zshrc` file and scroll down until you see the spot
where active plugins are defined. To add a new one, just type the name between
the parentheses, making sure to include a space between each name.

```
plugins=(git extract osx npm z)
```

To add a **custom plugin** you'll need to either use homebrew or manually copy the plugin files to the custom plugin path (see below).

_Note: ZSH bundled plugins are stored a- `/Users/paul/.oh-my-zsh/plugins`._

_Note: ZSH custom plugins are stored a- `/Users/paul/.oh-my-zsh/custom/plugins`._

Once you’ve added a plugin, you’ll need to either run `source ~/.zshrc` or open
a new terminal tab.

##### Recommended Oh-My-ZSH Plugins

###### Bundled Plugins

- extract
- git
- npm
- osx
- z

###### Custom Plugins

- zsh-autosuggestions _(can be installed via Homebrew. Remember to add the paths to these to in the `.zshrc` file.)_
- zsh-nvm
- zsh-syntax-highlighting _(can be installed via Homebrew. Remember to add the path to these in the `.zshrc` file.)_

_Note: The path to Homebrew installed custom plugins can be found at `/usr/local/share/<package-name>/<package-name>.zsh`._

### z

z isn’t part of Oh-My-ZSH, but it’s the perfect companion for anyone who heavily
uses the command line. The idea behind z is that it builds a list of your most
frequent and recent — “Frecent” — folders and allows you to jump to them quickly
in one command, rather than having to tab through a nested folder structure.

1.  z is included in the Oh-My-ZSH bundled plugins. Add it to the list of plugins in the `.zshrc` file.

```
plugins=(git extract osx npm z)
```

## Homebrew

### Installing Homebrew

The best way to install Homebrew is from [brew.sh][brew].

### Recommended Formulas

- ack - _a replacement for `grep`._
- composer
- curl
- git
- php
- php-code-sniffer
- trash-cli
- tree
- youtube-dl

_Note: see the ZSH section that may have plugins that can be installed via Homebrew._

_Note: Formulas are stored at `/usr/local/Cellar`._

### Recommended Casks

- hyper

_Note: Casks are stored at `/usr/local/Caskroom`._

_Note: You may need to add the path to your system PATH in the `.zshrc` file (e.g. `/usr/local/opt/php70/bin` in order for it to be used)._

## Node.js and npm

### Installing/managing Node.js via nvm

The best way to install and manage Node.js is using **Node Version Manager (nvm)**. When using ZSH and Oh-My-ZSH! it's easiest to install `nvm` via the Oh-My-ZSH! custom plugin `zsh-nvm`. If not you can install it via Homebrew.

_Note: The path for `nvm` installations of Node is `/Users/paul/.nvm/versions/node`._

_Note: nvm can be upgraded using the command `nvm upgrade`._

**Test command:** `node -v`

### Node Package Manager (npm)

Node comes with `npm` installed, however, `npm`
gets updated more frequently than Node does, so you'll want to make sure it's
the latest version. The following command will install/update npm globally.

```
npm install npm -g
```

**Test command:** `npm -v`

#### Possible Issues

If the test above doesn’t display a _npm_ version, you may have to add _npm_ to the
system PATH.

### Global Packages

Install the following npm packages globally:

- gulp-cli _- 1.2+ supports Gulp 3 and 4 out of the box._
- jasmine
- live-server
- modernizr _(run the following command to create the modernizr files based on
  the config file you specify_ - `modernizr -c modernizr-config.json`)
- webpack

**Example:** `npm install <package> -g`

_Note: Global packages are stored a- `/Users/paul/.nvm/versions/node/<node_version>/lib/node_modules`._

_Note: When you install global npm packages they will be installed for the current version of Node you have active. To reinstall packages you're using from another version of Node you can run the following command - `nvm reinstall-packages <version>`_

## Sass

_Note: Sass requires Ruby to be installed._

### Installing Sass

The following command will install Sass and any dependencies for you:

```
gem install sass
```

**Test command:** `sass -v`

## Composer

Install Composer globally using Homebrew.

_Note: The Homebrew Formula will be stored a- `/usr/local/Cellar/composer`._

Make sure you have the composer bin dir in your PATH as this is where the
_global_ composer packages will be installed and referenced from. The default
value is `~/.composer/vendor/bin/`, but you can check the value that you need to
use by running `composer global config bin-dir --absolute`.

Assuming the default bin dir you would add the following to your `.zshrc` (ZSH)
or your `.bash_profile` (Bash) or something equivalent to the shell you are
using.

For example in your `.zshrc` file:

```
export PATH=/Users/paul/.composer/vendor/bin:$PATH
```

## PHP_CodeSniffer and WordPress Coding Standards (with VS Code)

_Note: The following steps assume you have PHP installed and globally accessible
on your system._

### Global Install (system-wide)

#### PHP_CodeSniffer

_Note: You may need to install version 2.9 of PHPCS as version 3 doesn't seem to
work with the VS Code extension._

Install PHPCS globally using Homebrew (this is easier than using Composer for
the global installation).

#### WordPress Coding Standards

Clone a copy of the standards sniffer from GitHub. This assumes you’re working
out of `~/Dropbox/Misc/Front-end-dev/Coding_Standards` but you can install WPCS
anywhere you would like it to be referenced from.

```
git clone https://github.com/WordPress-Coding-Standards/WordPress-Coding-Standards.git wpcs
```

Then tell the global PHPCS about WPCS:

```
phpcs --config-set installed_paths ~/Dropbox/Misc/Front-end-dev/Coding_Standards/wpcs
```

_Note: This enters the path to the WPCS folder into the
`/usr/local/Cellar/php-code-sniffer/x.x.x/CodeSniffer.conf` file._

Finally, run `phpcs -i` and you should see the WordPress rules appear in the
available set. You should see something like the following:

```
The installed coding standards are MySource, PEAR, PHPCS, PSR1, PSR2, Squiz, Zend, WordPress, WordPress-Core, WordPress-Docs, WordPress-Extra and WordPress-VIP
```

#### VS Code User Settings

_Note: You may have to install the `phpcs` extension for this to work._

Finally, we need to let VS Code what we're going to be using to sniff out the
code in our project and what rules to use. Add the following to the
`settings.json` file.

```
"phpcs.enable":   true,
"phpcs.standard": "WordPress",
```

This will enable PHPCS and will also tell it to use the standard WordPress
ruleset. If this doesn't start working on your code automatically, then restart
VS Code.

### Local Install (project-by-project basis)

#### PHP_CodeSniffer

_Note: You may need to install version 2.9 of PHPCS as version 3 doesn't seem to
work with the VS Code extension._

To install PHP_CodeSniffer using Composer, you can issue the following command.
You need to be in the root of the project or you can use your code editor's
integrated terminal which should take you there by default.

```
composer require "squizlabs/php_codesniffer=*"
```

This will create `composer.json`, tell it where to locate PHP_CodeSniffer and
install it in a `vendor` directory. Once this is done, we need the WordPress
Coding Standard ruleset.

#### WordPress Coding Standards

Clone a copy of the standards sniffer from GitHub. This assumes you’re working
out of `~/Dropbox/Misc/Front-end-dev/Coding_Standards` but you can install WPCS
anywhere you would like it to be referenced from.

```
git clone https://github.com/WordPress-Coding-Standards/WordPress-Coding-Standards.git wpcs
```

Then tell PHPCS about WPCS:

Using the terminal, make sure that you're in your project's directory and then
issue the following command:

```
./vendor/bin/phpcs --config-set installed_paths ~/Dropbox/Misc/Front-end-dev/Coding_Standards/wpcs
```

This will tell your project's copy of PHPCS where the WordPress Coding Standards
are.

Finally, run `./vendor/bin/phpcs -i` and you should see the WordPress rules
appear in the available set. You should see something like the following:

```
The installed coding standards are MySource, PEAR, PHPCS, PSR1, PSR2, Squiz, Zend, WordPress, WordPress-Core, WordPress-Docs, WordPress-Extra and WordPress-VIP
```

#### VS Code User Settings

See the **VS Code User Settings** section in the global install instructions
above to setup VS Code to use PHPCS and WPCS.

## VS Code

### Packages

- ACF-Snippet
- Advanced New File
- Auto Close Tag
- Auto Rename Tag
- Better Comments
- Bracket Pair Colorizer
- Code Spell Checker
- colorize
- Debugger for Chrome
- ECMAScript Quotes Transformer
- EditorConfig for VS Code
- ESLint _- the npm package `eslint` is required to be installed in the workspace (recommended) or globally. The global `eslint` is needed for commands such as `eslint --init` to create an `.eslintrc.json` config file. See the extension instructions._
- Express
- Git History (git log)
- Git Lens
- Git Project Manager
- HTML Snippets
- HTML CSS Support
- IntelliSense for CSS class names
- Import Cost
- javascript console utils
- join-lines
- Markdown Toc
- markdownlint
- Multiple clipboards for VSCode
- npm
- npm Intellisense
- Path Intellisense
- PHP Intellisense - Crane
- phpcs
- Polacode
- PostCSS Sorting
- Prettier _- if you want Prettier to use `ESLint` and `Stylelint` rules, make sure you set this up in the VS Code settings. See the extension instructions._
- Project Manager
- Sort Lines
- SCSS Intellisense
- Settings Sync
- Sort JSON Objects
- stylelint _- this extension adds `stylelint` and reports errors in the 'Problems' tab. The npm package `stylelint-config-recommended` is required to be installed in the workspace if you want to extend these config presets. If you want to order CSS properties you need to install the `styleline-order` npm package in the workspace but note this requires the `stylelint` npm package to be installed in the workspace too._
- SVG
- SVG Viewer
- TODO Highlight
- Version Lens
- vscode-pandoc
- WordPress Snippet

### Themes

- Material Theme

### Icons

- Material Icon Theme
- vscode-icons

## SSH

### Generating a new SSH key

1. Run the following command in your terminal to create a new SSH key (private and public).

   `ssh-keygen -t rsa -b 4096`

_Note: The `-t rsa` forces the key to be in the RSA format._

_Note: The `-b 4096` forces the key to be 4096 bits._

_Note: You can add `-C "your comment here"` to add a comment to your generated key. For example, this could be an email address (e.g. `-C "yourname@yourdomain.com"`)._

1. When you're prompted to "Enter a file in which to save the key," press `Enter`. This accepts the default file location (i.e. `/Users/you/.ssh/`).

   `Enter a file in which to save the key (/Users/you/.ssh/id_rsa): [Press enter]`

   This will create a private key called `id_rsa` and a public key called `id_rsa.pub`.

   \_Note: If you want to give the key a different name add the `-f` option (e.g. `ssh-keygen -t rsa -b 4096 -f github_rsa`). Note this will create the the keys `hithub_rsa` and `github_rsa.pub` in the current working directory of the terminal.

1. At the prompt, type a secure passphrase.

   ```shell
   Enter passphrase (empty for no passphrase): [Type a passphrase]
   Enter same passphrase again: [Type passphrase again]
   ```

### Adding your SSH key to the ssh-agent

Before adding a new SSH key to the ssh-agent to manage your keys, you should have checked for existing SSH keys (i.e. `ls -al ~/.ssh`) and generated a new SSH key. When adding your SSH key to the agent, use the default macOS `ssh-add` command, and not an application installed by macports, homebrew, or some other external source.

1. If you're using macOS Sierra 10.12.2 or later, you will need to modify your `~/.ssh/config` file to automatically load keys into the ssh-agent and store passphrases in your keychain.

   ```
   Host *
   AddKeysToAgent yes
   UseKeychain yes
   IdentityFile ~/.ssh/id_rsa
   ```

1. Add your SSH private key to the ssh-agent and store your passphrase in the keychain. If you created your key with a different name, or if you are adding an existing key that has a different name, replace `id_rsa` in the command with the name of your private key file.

   `ssh-add -K ~/.ssh/id_rsa`

   _Note: The `-K` option is Apple's standard version of `ssh-add`, which stores the passphrase in your keychain for you when you add an ssh key to the ssh-agent._

   _Note: If you don't want to add the passphrase into the keychain you can use the standard `ssh-add ~/.ssh/id_rsa` command._

   _Note: If the ssh-agent isn't running you can start it up by running the command `eval "$(ssh-agent -s)"`._

### SSH config file

The SSH config file can help make life easier by setting options which help to automatically load keys into the ssh-agent, setting aliases to shorten what we have to type and automatically using passphrases stored in the keychain.

_Note: The config file can be edited or should be created at `~/.ssh/config`._

#### Config file example

```shell
Host *
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/id_rsa

# Example of using an alias. You can then connect with 'ssh cassify' in the terminal using the specified options.
Host cassify
  User cassify7
  HostName cassify.co.uk
  Port 18765
  IdentityFile ~/.ssh/cassify_rsa

# GitHub
Host github.com
  User git
  IdentityFile ~/.ssh/github_rsa
```

_Note: It's also possible to connect to [multiple GitHub accounts on a single machine][multiple-git]._

### Some ssh-add tricks

#### Listing

You can list the currently loaded keys with `-l` and `-L`. The former displays the keys fingerprints while the latter displays the entire public key. Both list the path of file the key came from, which it the only way I recognize them.

#### Deleting

`ssh-add -d file` removes the key the file from the agent. `ssh-add -D` clears out all keys, taking you back to square one.

#### Locking

You can simply run `ssh-add -D` to remove all of your keys from the Agent, but then you have to go through the trouble of adding them back. However, if you just want to step away and make sure your keys are protect, you can use `ssh-add -x`:

```shell
ssh-add -x
Enter lock password:
Again:
Agent locked.
```

The Agent still has your keys, but won’t allow them to be used until unlocked with `ssh-add -X`:

```shell
ssh-add -X
Enter lock password:
Agent unlocked.
```

#### Expiring

Instead of locking your keys, you can set an auto-expiry with `-t` after which the key will automatically be deleted from the agent:

```shell
ssh-add -t 60  ~/.ssh/random_rsa
Enter passphrase for /Users/spike/.ssh/random_rsa:
Identity added: /Users/spike/.ssh/random_rsa (/Users/spike/.ssh/random_rsa)
Lifetime set to 60 seconds
```

#### macOS Specific

On macOS `ssh-add` is integrated with the system keychain. If you give the `-K` option, as in `ssh-add -K`, when you add a key, that key’s password will be added to the keychain. As long as your keychain is unlocked, a key that has been stored in this way doesn’t require a password to be loaded into the agent.

All keys with their password stored in the keychain will automatically be loaded when you run `ssh-add -A`. This happens automatically on login.

I have mixed feeling about this feature, preloading your keys makes life easier, but it does remove a layer of security. If someone access your Mac, they get your keys. On the other hand, the probably get a lot of other things too. Typically, I take the lazy approach for everyday keys and keep the high-security ones out of the keychain.

When a password has been stored in keychain, `ssh-add -K -d key-file` both removes the key from the agent and removes it password from the keychain. Without `-K`, `-d` does not change the keychain and the key can be reloaded without a password. `-D` silently ignores `-K`.

[iterm]: https://www.iterm2.com/downloads.html 'iTerm'
[hyper]: https://hyper.is/ 'Hyper'
[zsh]: https://github.com/robbyrussell/oh-my-zsh/wiki/Installing-ZSH 'ZSH'
[oh-my-zsh]: https://github.com/robbyrussell/oh-my-zsh/ 'Oh-My-ZSH'
[oh-my-zsh-plugins]: https://github.com/robbyrussell/oh-my-zsh/wiki/Plugins 'Oh-My-ZSH Plugins'
[brew]: https://brew.sh/ 'Homebrew'
[wpcs&phpcs]: https://github.com/tommcfarlin/phpcs-wpcs-vscode 'WPCS and PHPCS'
[multiple-git]: https://medium.freecodecamp.org/manage-multiple-github-accounts-the-ssh-way-2dadc30ccaca 'How to manage multiple GitHub accounts on a single machine with SSH keys'
