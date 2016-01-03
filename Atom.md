# Atom
## Installation
Use a [PPA](http://www.webupd8.org/2014/06/atom-text-editor-available-for-linux.html) to install the most up-to-date version:

```bash
sudo add-apt-repository ppa:webupd8team/atom
sudo apt-get update
sudo apt-get install atom
```

## Atom packages
* install [git-control](https://atom.io/packages/git-control) to retrieve and push code editions to the central repository
* [markdown-preview](https://atom.io/packages/markdown-preview) is usually already installed
* [language-docker](https://atom.io/packages/language-docker) to edit `Dockerfile` files
* uninstall/disable `language-c`, `language-csharp` (many more could be disabled) for speed improvement, `metrics` to disable the Google Analytics tracking of Atom use Settings:
* `Settings` section:
  * Show Line Numbers
  * Soft Tabs
  * Font Size: 15 (suggestion)
  * Tab Length: 4
  * make sure that the `Ensure Single Trailing Newline` checkbox of the `whitespace` package is checked to make Atom add a newline character at the end of edited files
