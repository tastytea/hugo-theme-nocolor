# nocolor

**nocolor** is a [Hugo](https://gohugo.io/) theme with no predefined colors and
minimal styling. It is based on [Slick](https://github.com/spookey/slick).

## Features

* Supports taxonomies of tags, categories and series with their own pages.
* RSS Feed with complete entries.
* [Open Graph](http://ogp.me/), [Schema.org](https://schema.org/) and [Twitter
  Cards](https://developer.twitter.com/en/docs/tweets/optimize-with-cards/overview/abouts-cards.html)
  support.
* Fully customizable menu entries.
* No JavaScript, no bundled fonts, no external requests.
* Ability to inject own CSS file.

## Installation

``` shell
git submodule add --branch main https://schlomp.space/tastytea/hugo-theme-nocolor.git themes/nocolor
echo 'theme = "nocolor"' >> config.toml
```

Update with `git submodule update --remote`. If you don't keep your blog in a
git repository, install it with `git clone
https://schlomp.space/tastytea/hugo-theme-nocolor.git themes/nocolor` or unpack
the
[archive](https://schlomp.space/tastytea/hugo-theme-nocolor/archive/main.tar.gz)
into `themes/nocolor`.

### Breaking changes:

- 2021-09-25: Don't automatically add RSS hyperlink.

## Configuration & Modification

Please take a look at the [configuration example for
Slick](https://github.com/spookey/slick/blob/main/_sites/example/config.toml).
It is valid for nocolor too, with these exceptions:

* `favicon` and `css` have to be in in the assets folder.

You can add things to the end of the `<head>` section by overwriting the partial
template `extra_head.html` or above the footer by overwriting
`extra_foot.html`. The common way to do it is to create
`layouts/partials/extra_head.html` or `layouts/partials/extra_foot.html`,
respectively.

### Custom ARIA labels

Some elements can't be labeled by default because we don't know what's going to
be in it. Custom [ARIA
labels](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Roles/Navigation_Role)
are supported for the top menu and the bottom menu.

`config.toml`:
``` toml
[params]
    [params.aria]
        menu_top = "Main"
        menu_bottom = "Contact"
```

### Syntax highlighting with Asciidoctor

If you want source code highlighting with AsciiDoc, you'll need pygmentize from
the package [pygments](https://pygments.org/). Set this in your config file:

`config.toml`:
``` toml
pygmentsCodefences = true
pygmentsCodeFencesGuessSyntax = false
pygmentsUseClasses = true
```

Run `pygmentize -L styles` for a list of available styles and generate a CSS
file:

``` shell
pygmentize -f html -S <style> -a .highlight \
           | grep -v '^[^\.]' | sed -E 's/ \.(\w+) \{/ \.tok-\1 {/' > static/syntax.css
```

And add `:source-highlighter: pygments` at the top of your posts, below the
front matter. Make sure to include the generated CSS file. You can also set the
`source-highlighter` attribute in your config file.[^1]

### Table of contents

Table of contents are only written when the word count exceeds 400 and the `toc`
field in your content’s front matter is set to true. See [the Hugo
documentation](https://gohugo.io/content-management/toc) for details. You can
overwrite the template by adding the file `layouts/partials/toc.html` to your
blog.

## Screenshots

[![Screenshot](https://schlomp.space/tastytea/hugo-theme-nocolor/raw/branch/main/images/tn.png)](https://schlomp.space/tastytea/hugo-theme-nocolor/raw/branch/main/images/screenshot.png)

## Contributing

See <https://schlomp.space/tastytea/hugo-theme-nocolor/src/branch/main/CONTRIBUTING.adoc>.

[^1]: https://gohugo.io/content-management/formats/#external-helper-asciidoctor
