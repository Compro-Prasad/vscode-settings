# Visual Studio Code Settings

These are my [Visual Studio Code](https://code.visualstudio.com/) settings.

## Installation Instructions

I'm making use of symlinks to point my VSCode settings to my actual dev folder.
To make it easier to configure this, I've based my Rakefile off of what I've
seen in many other dotfiles. To install, just run:

```sh
rake install
```

## Synchronizing Extensions

Visual Studio Code extensions are currently tracked fully by them being
dropped in the `/.vscode/extensions` directory. To keep a list of only the
extensions, you need to sync them down to `extensions.json`. To do this,
just run:

```sh
rake sync
```
