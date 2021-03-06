# Contributing to electron.atom.io

:+1::tada: First off, thanks for taking the time to contribute! :tada::+1:

The following is a set of guidelines for contributing to electron.atom.io on GitHub. These are just guidelines, not rules, use your best judgment and feel free to propose changes to this document in a pull request.

## Issues & Pull Requests

* If you're not sure about adding something, open an issue to discuss it.
* Feel free to open a Pull Request early so that a discussion can be had as changes are developed.
* Include screenshots and animated gifs of your changes whenever possible.
* End files with a newline.


## Adding an app or project to the site

If you have an Electron application or project you'd like to see added, please open a pull request!

Add your app to the list by editing [index.html](/index.html). **Please add your app at the bottom of the list**. Here's a sample of the HTML markup to use:

```html
<a href='https://yourproject.com/' target='_blank' title='Your Project'>
  <img class='other-logo' src='../images/yourproject.png' alt='Your Project'>
</a>
```

## Documentation

The documentation on this site is pulled directly from the `atom/electron` repository's `docs` directory. Contributions to the documentation should be made there: [atom/electron](https://github.com/atom/electron/tree/master/docs).
