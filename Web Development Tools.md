# Web Development Tools

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
  - [Packages (replaced by built-in functionality)](#packages-replaced-by-built-in-functionality)
  - [Themes](#themes)
  - [Icons](#icons)
- [Debugging](#debugging)
  - [Debugging Modern JavaScript](#debugging-modern-javascript)
  - [Debugging with Chrome & React.js Framework](#debugging-with-chrome--reactjs-framework)
  - [Node.js](#nodejs)
  - [VS Code WordPress Debugging Setup using Xdebug and Local by Flywheel](#vs-code-wordpress-debugging-setup-using-xdebug-and-local-by-flywheel)
- [SSH](#ssh)
  - [Generating a new SSH key](#generating-a-new-ssh-key)
  - [Adding your SSH key to the ssh-agent](#adding-your-ssh-key-to-the-ssh-agent)
  - [SSH config file](#ssh-config-file)
  - [Some `ssh-add` tricks](#some-ssh-add-tricks)

## Command-Line Tools

### Important Info

#### System Path

The file which lists all of the paths in your system \$PATH can be found at
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

ZSH is a popular alternative to the Bash shell. ZSH is installed on macOS by default but you may wish to install the most up to date version, you can do this using Homebrew.

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

- zsh-autosuggestions - _(can be installed via Homebrew. Remember to add the paths to this to in the `.zshrc` file.)_
- zsh-nvm
- zsh-syntax-highlighting - _(can be installed via Homebrew. Remember to add the path to this in the `.zshrc` file.)_

_Note: The path to Homebrew installed custom plugins can be found at `/usr/local/share/<package-name>/<package-name>.zsh`._

### z

z isn’t part of Oh-My-ZSH, but it’s the perfect companion for anyone who heavily
uses the command line. The idea behind z is that it builds a list of your most
frequent and recent — “Frecent” — folders and allows you to jump to them quickly
in one command, rather than having to tab through a nested folder structure.

1. `z` is included in the Oh-My-ZSH bundled plugins. Add it to the list of plugins in the `.zshrc` file.

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
- qlImageSize ([manual install][cask-qlimagesize])
- [Quick Look plugins][cask-quick-look]

_Note: Casks are stored at `/usr/local/Caskroom`._

_Note: You may need to add the path to your system PATH in the `.zshrc` file (e.g. `/usr/local/opt/php70/bin` in order for it to be used)._

## Node.js and npm

### Installing/managing Node.js via nvm

The best way to install and manage Node.js is using **Node Version Manager (nvm)**. When using ZSH and Oh-My-ZSH! it's easiest to install `nvm` via the Oh-My-ZSH! custom plugin `zsh-nvm`. If not you can install it via Homebrew but be careful as it is not officially supported.

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
- eslint
- jasmine
- live-server
- modernizr _(run the following command to create the modernizr files based on
  the config file you specify_ - `modernizr -c modernizr-config.json`)
- parcel
- webpack

**Example:** `npm install <package> -g`

_Note: Assuming you are using nvm to manage Node versions, the global `npm` packages are stored at- `/Users/paul/.nvm/versions/node/<node_version>/lib/node_modules`._

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

Install PHPCS globally using Composer.

```
composer global require "squizlabs/php_codesniffer=*"
```

This will install PHPCS in the `vendor` folder of the composer global directory `/Users/paul/.composer`. It will also update `composer.json` to tell it where to locate PHPCS. Once this is done, we need the WordPress Coding Standard ruleset.

#### WordPress Coding Standards

Clone a copy of the standards sniffer from GitHub. This assumes you’re working out of `~/Dropbox/Misc/Front-end-dev/Coding_Standards` but you can install WPCS
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

_Note: You will need to install the `phpcs` and `phpcbf` extensions for this to work._

_Note: The **global** `phpcs` and `phpcbf` will be used._

Finally, we need to let VS Code what we're going to be using to sniff out the
code in our project and what rules to use. Add the following to the
`settings.json` file.

```
"phpcs.enable": true,
"phpcs.ignorePatterns": ["*/vendor/*", "*/vendors/*"],
"phpcs.standard": "WordPress",
"phpcbf.enable": true,
"phpcbf.onsave": true,
"phpcbf.standard": "WordPress"
```

This will enable PHPCS and PHPCBF and will also tell them to use the standard WordPress ruleset. If this doesn't start working on your code automatically, then restart VS Code.

### Local Install (project-by-project basis)

#### PHP_CodeSniffer

To install PHP_CodeSniffer using Composer, you can issue the following command.
You need to be in the root of the project or you can use your code editor's
integrated terminal which should take you there by default.

```
composer require "squizlabs/php_codesniffer=*"
```

This will install PHPCS in the `vendor` folder of the working directory/workspace. It will also create a `composer.json` file and update it to tell it where to locate PHPCS. Once this is done, we need the WordPress Coding Standard ruleset.

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

_Note: You will need to install the `phpcs` and `phpcbf` extensions for this to work._

_Note: The **local** `phpcs` and `phpcbf` will be used._

Finally, we need to let VS Code what we're going to be using to sniff out the
code in our project and what rules to use. Add the following to the
`settings.json` file.

```
"phpcs.enable": true,
"phpcs.executablePath": "./vendor/bin/phpcs",
"phpcs.ignorePatterns": ["*/vendor/*", "*/vendors/*"],
"phpcs.standard": "WordPress",
"phpcbf.enable": true,
"phpcbf.executablePath": "./vendor/bin/phpcbf",
"phpcbf.onsave": true,
"phpcbf.standard": "WordPress",
```

This will enable PHPCS and PHPCBF and will also tell them to use the standard WordPress ruleset. If this doesn't start working on your code automatically, then restart VS Code.

## VS Code

### Extensions

- ACF-Snippet
- Advanced New File
- Apache Conf
- Apache Conf Snippets
- Auto Close Tag
- Auto Rename Tag
- Better Align
- Better Comments
- Bracket Pair Colorizer
- change-case
- Code Runner
- Code Spell Checker
- colorize
- Complete JSDoc Tags
- CSS Peek
- Debugger for Chrome
- ECMAScript Quotes Transformer
- EditorConfig for VS Code
- ESLint _- the npm package `eslint` is required to be installed in the workspace (recommended) or globally. The global `eslint` is useful for commands such as `eslint --init` to create an `.eslintrc.json` config file. See the extension instructions._
- expand-region
- Express
- File Utils
- Git Project Manager
- Gitconfig Syntax
- GitHub Pull Requests
- gitignore
- GitLens
- Highlight Matching Tag
- HTML CSS Support
- HTMLHint
- Import Cost
- indent-rainbow
- Insert Numbers
- JavaScript (ES6) code snippets
- javascript console utils
- JavaScript Snippet Pack
- jQuery Code Snippets
- lit-html
- macros
- Markdown All in One
- markdownlint
- Node.js Modules Intellisense
- npm
- npm Intellisense
- Output Colorizer
- Path Intellisense
- PHP Debug
- PHP Intelephense
- PHP Intellisense
- phpcbf _-the actual tool `phpcbf` is installed as part of `phpcs`._
- phpcs
- Polacode
- PostCSS Sorting
- Prettier _- if you want Prettier to use `ESLint` and `Stylelint` rules, make sure you set this up in the VS Code settings. See the extension instructions._
- Project Manager
- pug
- Pug to HTML
- puglint
- Quokka.js
- React Native Tools
- Reactjs code snippets
- Save and Run
- SCSS IntelliSense
- Search WordPress Docs
- Settings Sync
- snippet-creator
- Sort JSON Objects
- Sort lines
- stylelint _- this extension adds `stylelint` and reports errors in the 'Problems' tab. The npm package `stylelint-config-recommended` is required to be installed in the workspace if you want to extend these config presets. If you want to order CSS properties you need to install the `styleline-order` npm package in the workspace but note this requires the `stylelint` npm package to be installed in the workspace too._
- SVG
- SVG Viewer
- TODO Highlight
- Trailing Spaces
- Turbo Console Log
- Version Lens
- vscode-faker
- vscode-pandoc
- Wakatime
- Word Count
- WordPress Snippets

### Extensions (replaced by built-in functionality)

- IntelliSense for CSS class names
- HTML Snippets

### Themes

- Material Theme

### Icons

- Material Icon Theme
- vscode-icons

## Debugging

### Debugging Modern JavaScript

_Note: These notes are taken from the [VS Code Power User][vscode-pro] course by [Ahmad Awais][ahmad-awais]._

Debug modern JavaScript with this VS Code and Babel recipe.

#### 1. Init a module (without it asking any questions)

```sh
npm init -y
```

#### 2. Babel setup

```sh
npm i -D babel-cli babel-core babel-preset-env
```

#### 3. Add `.babelrc`

```sh
touch .babelrc
```

#### 4. Edit `.babelrc`

```json
{
  "presets": ["env"]
}
```

#### 5. The `package.json` file looks like

```json
{
  "name": "vscodepro",
  "description": "VSCode.pro for Power Users",
  "version": "1.0.0",
  "author": "AhmadAwais",
  "license": "MIT",
  "main": "index.js",
  "scripts": {
    "start": "babel-node index.js",
    "debug": "babel-node debug index.js"
  },
  "devDependencies": {
    "babel-cli": "^6.26.0",
    "babel-core": "^6.26.3",
    "babel-preset-env": "^1.7.0"
  }
}
```

#### 6. My `.vscode/launch.json` file

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "type": "node",
      "request": "attach",
      "name": "Attach",
      "restart": true,
      "port": 9229
    },
    {
      "type": "node",
      "request": "launch",
      "protocol": "inspector",
      "name": "ES6 Debugger",
      "program": "${workspaceFolder}/index.js",
      "runtimeExecutable": "${workspaceRoot}/node_modules/.bin/babel-node",
      "runtimeArgs": ["--presets", "env"]
    }
  ]
}
```

### Debugging with Chrome & React.js Framework

1. This requires that you have the [Debugger for Chrome][debugger-for-chrome] VS Code extension installed.

2. Create a `launch.json` file.

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "type": "chrome",
      "request": "launch",
      "name": "Chrome + React",
      "url": "http://localhost:3000",
      "webRoot": "${workspaceFolder}/src"
    }
  ]
}
```

### Node.js

See the [Node.js debugging in VS Code with Nodemon][nodejs-vscode-debugging] Github repository for more details.

### VS Code WordPress Debugging Setup using Xdebug and Local by Flywheel

_Note: These notes are taken from the [VS Code Power User][vscode-pro] course by [Ahmad Awais][ahmad-awais]._

#### TL;DR

- Make sure your `Local by Flywheel` WordPress install is a custom install.
- Configure `xdebug.remote_autostart = 1` in the `php.ini` file.
- Restart your site container in `Local by Flywheel` to apply new settings.
- Install VS Code `PHP Debug` extension.
- Add PHP Debugger Configuration with an extra property for the `Listen for Xdebug` section i.e. `"pathMappings": {"/app/public/wp-content/themes/theme-name": "${workspaceFolder}"}`.

#### Detailed Tutorial

Here're are some easy steps to follow to make sure you can debug WordPress in Local by Flywheel with VS Code:

##### Custom WordPress Install

_Note: Make sure your `Local by Flywheel` WordPress install is using a custom local environment._

- Flywheel Local has Xdebug installed by default if you choose “Custom” instead of “Preferred” when setting up a new local environment.
- If you are not running a custom local environment you can just export your site, import it back in and this time choose “Custom”. It's possible to change the local environment from within the settings but this sometimes causes problems.

##### Configure Xdebug

Now that we are using a custom local environment we need to configure Xdebug.

- Go to your local WordPress install path E.g. `/PATH_WHERE_YOU_INSTALLED_WORDPRESS/conf/php/7.x.x/php.ini`.
- Search for the `[Xdebug]` section.
- Add the following line in this section.

```ini
xdebug.remote_autostart = 1
```

_Note: While only the above option is required but some 3rd party extension/plugin for local can sometimes change things so make sure in the `[Xdebug]` section all the following settings are set to `1` (only if your debugger is not working)._

```ini
xdebug.scream = 1
xdebug.remote_enable = 1
xdebug.show_local_vars = 1
xdebug.remote_autostart = 1
xdebug.remote_connect_back = 1
```

Save the `php.ini` file.

##### Restart The Site

Restart your site container in `Local by Flywheel` to apply new settings.

- On the left side menu, right click on your site.
- Select `Restart` option to restart the site.

##### Visual Studio Code Configuration

Let's start configuration of VS Code:

- First of all, install [PHP Debug][php-debug] extension.
- Open your Local WordPress site project folder in VS Code. You should open theme folder i.e. `/PATH_WHERE_YOU_INSTALLED_WORDPRESS/app/public/wp-content/themes/theme-name`.
- Go to the Debug view in VS Code `COMMAND (⌘) + SHIFT (⇧) + D`.
- Click “Add configuration” from the top toolbar.
- Select `PHP` and add the configuration.
- In the `.vscode/launch.json` file that was created inside the `Listen for Xdebug` section add `"pathMappings": {"/app/public/wp-content/themes/theme-name": "${workspaceFolder}"}`.

In short, your debug `launch.json` file will look like this:

```json
{
  // Use IntelliSense to learn about possible attributes.
  // Hover to view descriptions of existing attributes.
  // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Listen for Xdebug",
      "type": "php",
      "request": "launch",
      "port": 9000,
      "pathMappings": {
        "/app/public/wp-content/themes/theme-name": "${workspaceFolder}"
      }
    },
    {
      "name": "Launch currently open script",
      "type": "php",
      "request": "launch",
      "program": "${file}",
      "cwd": "${fileDirname}",
      "port": 9000
    }
  ]
}
```

##### Debug Your WordPress

Now go ahead and debug your WordPress app/plugin/theme.

- Click the play button next to “Listen for Xdebug” in the top debug bar.
- Create a breakpoint in your PHP code e.g. add this line and a breakpoint`<?php $true_story = 'Ahmad is cool and VS code.pro is awesome!'; ?>` to `header.php` of your theme.
- Browse your site and VS Code should pop up showing all your debug info.

#### Extra Plugin (optional)

You can also install a local plugin called [local-addon-xdebug-control][local-addon-xdebug-control] for UI based control of Xdebug settings in your `Local by Flywheel` software.

_Note: Make sure everything is set to yes for a sane debugging experience._

![Add-on](https://on.ahmda.ws/9155be150de8/c)

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

   \_Note: If you want to give the key a different name add the `-f` option (e.g. `ssh-keygen -t rsa -b 4096 -f github_rsa`). Note this will create the the keys `github_rsa` and `github_rsa.pub` in the current working directory of the terminal.

1. At the prompt, type a secure passphrase.

   ```shell
   Enter passphrase (empty for no passphrase): [Type a passphrase]
   Enter same passphrase again: [Type passphrase again]
   ```

### Adding your SSH key to the ssh-agent

Before adding a new SSH key to the ssh-agent to manage your keys, you should have checked for existing SSH keys (i.e. `ls -al ~/.ssh`) or generated a new SSH key. When adding your SSH key to the agent, use the default macOS `ssh-add` command, and not an application installed by macports, homebrew, or some other external source.

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

Example of using an alias. You can then connect with 'ssh cassify' in the terminal using the specified options.

```shell
# Web Hosting
Host somealias
  User someuser
  HostName example.co.uk
  Port 18765

# GitHub (Personal)
Host github.com
   HostName github.com
   User git

# GitHub (Work Account)
Host github.com-workaccount
   HostName github.com
   User git
   IdentityFile ~/.ssh/work_rsa

# Fallback for all other SSH connections. The below settings wil also be applied to the above if something has been omitted (e.g. IdentityFile, UseKeyChain, etc.)
Host *
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/id_rsa
```

_Note: Learn more about how to connect to [multiple GitHub accounts on a single machine][multiple-git]._

### Some `ssh-add` tricks

#### Listing

You can list the currently loaded keys with `-l` and `-L`. The former displays the keys fingerprints while the latter displays the entire public key.

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
[vscode-pro]: https://vscode.pro/ 'VS Code Power User - Learn Visual Studio Code'
[ahmad-awais]: https://ahmadawais.com/ 'Ahmad Awais - Developer Advocate for JavaScript & Open Source'
[php-debug]: https://marketplace.visualstudio.com/items?itemName=felixfbecker.php-debug 'PHP Debug Adapter for Visual Studio Code'
[local-addon-xdebug-control]: https://github.com/lucatume/local-addon-xdebug-control 'A Local by Flywheel addon to manage XDebug settings through the UI.'
[nodejs-vscode-debugging]: https://github.com/Microsoft/vscode-recipes/tree/master/nodemon
[debugger-for-chrome]: https://marketplace.visualstudio.com/items?itemName=msjsdiag.debugger-for-chrome 'A VS Code extension to debug your JavaScript code in the Google Chrome browser'
[cask-quick-look]: https://github.com/sindresorhus/quick-look-plugins 'Quick Look plugins'
[cask-qlimagesize]: https://github.com/L1cardo/qlImageSize 'qlImageSize'
