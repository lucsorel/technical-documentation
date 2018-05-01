# Atom
## Installation
Use a [PPA](http://www.webupd8.org/2014/06/atom-text-editor-available-for-linux.html) to install the most up-to-date version:

```bash
sudo add-apt-repository ppa:webupd8team/atom
sudo apt-get update
sudo apt-get install atom
```

## Atom packages
Some packages I use:
* [markdown-preview](https://atom.io/packages/markdown-preview) is usually already installed to view and edit markdown files
* version control:
  * [git-control](https://atom.io/packages/git-control) to retrieve/push editions from/to the central repository
  * [blame](https://atom.io/packages/blame) to view the commit details of each line. Setting a custom repository URL may be necessary when using a custom git config to handle multiple ssh keys
* [file-icons](https://atom.io/packages/file-icons) with the `coloured` checkbox unticked
* [linter-eslint](https://atom.io/packages/linter-eslint) to use eslint rules and display linting failures. Tick the `Fix on save` checkbox to fix the indentation and the rules that eslint can apply by itself
* minimap:
  * [minimap](https://atom.io/packages/minimap) to display a snapshot of the displayed source code
  * [minimap-autohide](https://atom.io/packages/minimap-autohide) so that minimap displays on scroll and hides when coding
  * [minimap-linter](https://atom.io/packages/minimap-linter) to display linting errors in the minimap
* language packages:
  * [language-docker](https://atom.io/packages/language-docker) to edit `Dockerfile` files
  * [language-r](https://atom.io/packages/language-r) to edit R scripts

Some packages I removed/disabled for speed improvement:
* uninstall/disable `language-c`, `language-csharp` (many more could be disabled) for speed improvement, `metrics` to disable the Google Analytics tracking of Atom use

Settings:
* Show Line Numbers
* Soft Tabs
* Font Size: 15 (suggestion)
* Tab Length: 4
* make sure that the `Ensure Single Trailing Newline` checkbox of the `whitespace` package is checked to make Atom add a newline character at the end of edited files

## Keyboard shortcuts
Editing the `keymap.cson` allows to add some shortcuts:
* reveal opened file in tree view
```cson
'atom-text-editor':
  'ctrl-alt-/': 'tree-view:reveal-active-file'
```

## Snippets
Snippets are code templates that can be triggered when starting to type a `code prefix` and pressing the `tab` key to validate a suggested snippet. Here are the ones I often use - some refer to the [i18n-express](https://github.com/lucsorel/i18n-express) project I developed ("*an ExpressJs middleware to internationalize templates and manage URL routing for internationalized web applications*"):

### Generic JS snippets

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
	'Use strict':
		'prefix': 'usestrict'
		'body': '\'use strict\';\n'
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
	'Insecable space':
		'prefix': 'nbsp'
		'body': '&nbsp;'
	'Html entity':
		'prefix': 'ent'
		'body': '&$1;'
```

### I18n-express snippets

```yaml
'.text.html':
	'i18n-express key':
		'prefix': 'ikh'
		'body': '__{$1}'
	'i18n-express key with param':
		'prefix': 'ikhp'
		'body': '__{$1%%$2%%}'
'.source.json':
	'i18n-express key':
		'prefix': 'ikj'
		'body': '"$1": "$2",'
	'i18n-express message parameter':
		'prefix': 'ipj'
		'body': '__{$1:$2}'
```

### AngularJS 1.x snippets

```yaml
'.source.js':
    'AngularJS injection':
        'prefix': 'inject'
        'body': '$inject = [\'$1\'];'
    'AngularJS $timeout service':
        'prefix': 'timeout-ng'
        'body': "$timeout($2, $1);"
    'AngularJS provider with dependencies':
        'prefix': 'provider-ng'
        'body': """
        $1.$inject = [\'$2\'];
        function $1($2) {
            $3
        });
        """
'.text.html':
    'ng-class':
        'prefix': 'ngcss'
        'body': 'ng-class="$1"'
    'ng-click':
        'prefix': 'ngck'
        'body': 'ng-click="$1"'
    'ng-change':
        'prefix': 'ngcg'
        'body': 'ng-change="$1"'
    'ng-if':
        'prefix': 'ngi'
        'body': 'ng-if="$1"'
    'ng-model':
        'prefix': 'ngm'
        'body': 'ng-model="$1"'
    'ng-show':
        'prefix': 'ngs'
        'body': 'ng-show="$1"'
    'ng-switch':
        'prefix': 'ngsw'
        'body': 'ng-switch="$1"'
    'ng-switch-when':
        'prefix': 'ngsww'
        'body': 'ng-switch-when="$1"'
    'ng-switch-default':
        'prefix': 'ngswd'
        'body': 'ng-switch-default=""'
```

### Thymeleaf snippets
```yaml
'.text.html':
    'Thymeleaf comment':
        'prefix': 'th-comment'
        'body': '<!--/* $1 */-->'
    'Thymeleaf if':
        'prefix': 'th-if'
        'body': 'th:if="${$1}"'
    'Thymeleaf attributes':
        'prefix': 'th-attr'
        'body': 'th:attr="$1=${$2}"'
    'Thymeleaf with':
        'prefix': 'th-with'
        'body': 'th:with="$1=${$2}"'
    'Thymeleaf class':
        'prefix': 'th-class'
        'body': 'th:class="${$1}" ? \'$2\' : \'$3\''
    'Thymeleaf image src':
        'prefix': 'th-src'
        'body': 'th:src="@{$1}"'
```
