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

## Snippets
Snippets are code templates that can be triggered when starting to type a `code prefix` and pressing the `tab` key to validate a suggested snippet. Here are the ones I often use - some refer to the [i18n-express](https://github.com/lucsorel/i18n-express) project I developed ("*an ExpressJs middleware to internationalize templates and manage URL routing for internationalized web applications*"):
```yaml
'.source.js':
	'Console log':
    	'prefix': 'clog'
    	'body': 'console.log(${1:\'\'});$2'
	'If':
		'prefix': 'if'
		'body': """
			if ($1) {
				$2
			}
		"""
	'Elseif':
		'prefix': 'elif'
		'body': """
			else if ($1) {
				$2
			}
		"""
	'Else':
		'prefix': 'el'
		'body': """
			else {
				$1
			}
		"""
	'If else':
		'prefix': 'ifel'
		'body': """
			if ($1) {
				$2
			}
			else {
				$3
			}
		"""
	'If elseif':
		'prefix': 'ifelif'
		'body': """
			if ($1) {
				$2
			}
			else if ($3) {
				$4
			}
		"""
	'If null':
		'prefix': 'ifn'
		'body': """
			if (null === $1) {
				$2
			}
		"""
	'If not null':
		'prefix': 'ifnn'
		'body': """
			if (null !== $1) {
				$2
			}
		"""
	'Function':
		'prefix': 'function'
		'body': """
		function($1) {
			$2
		}
		"""
	'Immediately-invoked function expression':
		'prefix': 'iif'
		'body': """
		(function() {
			'use strict';
			$1
		}());
		"""
	'Module exports':
		'prefix': 'mexp'
		'body': 'module.exports = $1;'
	'Describe (unit-testing)':
		'prefix': 'describe'
		'body': """
		describe('# $1', function() {
			$2
		});
		"""
	'It (unit-testing)':
		'prefix': 'it'
		'body': """
		it('$1', function() {
			$2
		});
		"""
	'Assert equal (unit-testing)':
		'prefix': 'asseq'
		'body': "assert.equal($1, $2, '$3');"
	'Assert true (unit-testing)':
		'prefix': 'asstrue'
		'body': "assert.equal($1, true, '$2');"
	'Assert false (unit-testing)':
		'prefix': 'assfalse'
		'body': "assert.equal($1, false, '$2');"
	'Block comment (class/function)':
		'prefix': 'commentblock'
		'body': """
		/**
		 * $1
		 *
		 * @param $2
		 * @return $3
		 */
		"""
'.text.html':
	'i18n-express key':
		'prefix': 'ikh'
		'body': '__{$1}'
	'i18n-express key with param':
		'prefix': 'ikhp'
		'body': '__{$1%%$2%%}'
	'Insecable space':
		'prefix': 'nbsp'
		'body': '&nbsp;'
	'Html entity':
		'prefix': 'ent'
		'body': '&$1;'
'.source.json':
	'i18n-express key':
		'prefix': 'ikj'
		'body': '"$1": "$2",'
	'i18n-express message parameter':
		'prefix': 'ipj'
		'body': '__{$1:$2}'
```
