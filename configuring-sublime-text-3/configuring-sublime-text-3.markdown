---
date: 2013-12-19
---
# Configuring Sublime Text 3

Some days ago I stumbled across [this website](http://www.caniswitchtosublimetext3.com/), which checks if your installed Sublime plugins are compatible with Sublime Text 3. As all of mine were already compatible I made the switch. Nevertheless I had to spend some time migrating, because there are some differences in setting up Sublime’s snippets and SublimeLinter.

## Disabling default snippets

By default Sublime has some snippets installed that you may find useful. Personally I like to use my own, therefore I disable the pre-installed ones. In Sublime Text 2 this could be done by deleting the snippets from the `Packages` folder. Unfortunately updates reverted those changes.

Sublime Text 3 handles its internal snippets differently. They are now stored directly as bundled packages inside of the main app, but can be overwritten by adding a snippet with the same name in the Packages folder. To extract all snippets of a language there is a package called __PackageResourceViewer__, which is available in Package Control. Simply install the package, search for the “PackageResourceViewer: Extract Package” command and choose the language with the snippets you want to edit or disable.

All files inside this package will now be copied to your Packages folder: `~/Library/Application Support/Sublime Text 3/Packages/`. Now you can edit the pre-installed snippets and completions by opening files with the extensions `.sublime-snippet` or `.sublime-completions`. Sometimes there are also some completions stored as python files, for example `css_completions.py`.

If you simply want to disable the default auto-completions, open these files and remove all content. Empty files are evaluated as if there is no snippet/completion. To benefit from future updates, I recommend deleting all other files that have been extracted to your Packages folder, as these are language definitions and settings.

## SublimeLinter3

I use SublimeLinter for JavaScript programming. Its latest update, which only works with Sublime Text 3, has some major changes. The main package does now operate as a framework for different linters and each linter has its own package in Package Control.

To use jshint you have to install the __SublimeLinter__ and __SublimeLinter-jshint__ package. [SublimeLinter-jshint](https://github.com/SublimeLinter/SublimeLinter-jshint) requires `node` and `jshint` to be installed globally. If you use `zsh` and `nvm` like I do, you’ll also have to add your current node version to your PATH in a .zshenv file, e.g. `export PATH=$PATH:/Users/max/.nvm/v0.10.26/bin`. Otherwise SublimeLinter won’t find jshint. There also is a path setting for different operating systems in the new `SublimeLinter.sublime-settings` file, but adding the path there didn’t work for me.
