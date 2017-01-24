# Visual Studio Code Settings

These are my [Visual Studio Code](https://code.visualstudio.com/) settings.

## Installation Instructions

I'm making use of symlinks to point my VSCode settings to my actual dev folder.
To make it easier to configure this, I've based my Rakefile off of what I've
seen in many other dotfiles. To install, just run:

```sh
rake install
```

## Still To Do

I'd like to keep my VSCode extensions in sync as well; however, VSCode
currently just keeps them in a directory (as opposed to having a file that
tracks them). This is fine, but I'd rather only keep a file of extension names
instead of the extensions themselves.

See below for notes:

```sh
code --list-extensions
# same list as...
ls ~/.vscode/extensions
```

* [x] either symlink the entire Code directory or individual settings, keybindings files plus snippets directory
* [ ] just track extensions in some file... json or yaml or whatever... then have a command to install/sync them
	* so, spin list-extensions and sync/compare with local file and install ones that don't exist
	* sort of like how that Emacs package thing worked???
