# Github responsive pages
Github webpages are not responsive, which is a shame. The solve that, follow [this workaround](https://github.com/mdo/github-wide):
* install the [Stylish](https://addons.mozilla.org/fr/firefox/addon/stylish/) Firefox extension (it also exists for Chromium)
* create a new style named `Github wide`
* copy-paste the [github-wide.css](https://github.com/mdo/github-wide/blob/master/github-wide.css) style sheet
* configure it so that it applies to the `github.com` domain:
```css
@namespace url(http://www.w3.org/1999/xhtml);

@-moz-document domain("github.com") {
    /* https://github.com/mdo/github-wide */
    .container {
      width: 100% !important;
      padding-left: 30px !important;
      padding-right: 30px !important;
    }
    /* ... */
    .commit-desc pre {
      max-width: none;
    }
}
```
