# Co-op

[![Issue Tracker][badge]][issues]

**Co-op** is a [Hugo] theme for creating a simple and accessible marketing site
with an optional blog.
It is typeset in [Overpass] by [Delve Fonts].

[![Screenshot][screenshot]][screenshot]

[badge]: https://img.shields.io/badge/issues-samwhited%2fco--op-green.svg?longCache=true&style=popout-square&label=todo
[issues]: https://todo.sr.ht/~samwhited/co-op
[Hugo]: https://gohugo.io/
[Overpass]: https://overpassfont.org/
[Delve Fonts]: https://www.delvefonts.com/
[screenshot]: https://git.sr.ht/~samwhited/co-op/blob/refs/heads/master/images/screenshot.png


## Configuration

For an examples of the following configuration, see [`exampleSite/config.toml`].

[`exampleSite/config.toml`]: https://git.sr.ht/~samwhited/co-op/tree/master/exampleSite/config.toml


### Site menu

The global menu can be tweaked by adding a menu called `main` in the site
config. For example:

```toml
[menu]

  [[menu.main]]
    identifier = "about"
    name = "About"
    url = "/about/"
    weight = 10
```


### Site params

In addition to the standard parameters, the site may be configured by setting
any of the following in the main config file:

**logo**: Path to the main logo to be shown in the header.

**description:** A description to be shown in the `description` and
`og:description` meta tags.

**contact.address:** A mailing address to show in the info bar at the top of the
page.

**contact.geo:** If specified along with `contact.address`, the address will
treat this as a safe URI (probably a link to a map or a `geo:` URI).

**contact.email:** An email address to link in the info bar at the top of the
page.

**contact.telephone:** A telephone number to show in the info bar at the top of
the page.

**contact.tel:** The path component of a `tel:` URI (just the number) which will
be linked if `contact.telephone` is specified.

**contact.muc:** An XMPP address to a multi-user chat room to be linked in the
info bar at the top of the page.

Any parameters that exist in the code but which are not documented here have not
been finalized and may be removed at any time without warning.


### Post params

In addition to the standard parameters, individual pages and blog posts may be
configured by setting any of the following parameters:

**description:** A description to be shown in the `description` and
`og:description` meta tags (overrides `.Site.Params.description`).

**tags:** A list of tags to apply to this page. If the page is a blog post, the
tags will be linked at the bottom of the post.

**noindex:** If set to anything but `false` adds a `noindex` meta tag to the
page.

The following apply to blog posts only:

**authors:** An array of author names (as strings) to be shown below this blog.

When creating a post with `hugo new post/<title>.md` the special post archetype
will be used which contains all available parameters in TOML format.
If you want the blog to show up under `/blog` instead of `/post`, add something
like the following to your `config.toml`:

```toml
[permalinks]
  post = "/blog/:slug"
```


### Styles

To change the style, the following CSS variables may be overridden by setting
them on the `:root` CSS element (default values are shown):

```css
:root {
	--color-accent: #BF3211;
	--color-accent-subtle: #D1D1D1;
	--color-caption-txt: #545454;
	--color-dark-bg: #232432;
	--color-dark-txt: #232432;
	--color-light-bg: #fcfcfc;
	--max-content-width: 900px;
}
```

To insert your custom CSS file after the main file loaded by the theme, create a
partial called `css.html`.
Any variables not listed here may be removed from the main CSS file at any time
without warning.


### Partials

The following partials may be overridden:

**addr.html:** prints `.address` with the link `.geo` if present. See also the
shortcode with the same name.

**css.html:** empty partial included immediately after the main CSS file.

**email.html:** creates a `mailto:` link to `.`. See also the shortcode with the
same name.

**fonts.html:** contains font loading (in case you want to load fonts from a CDN
instead of locally).

**footer.html:** the page footer; defaults to empty, this should probably
contain a single `<footer/>` element.

**head.html:** the entire `<head/>` element; this should probably be left alone.

**header.html:** the page header; shows the logo and navigation by default.

**icons.html:** the icon area at the end of the info bar. This is normally a
single span with the `icons` class applied and contains a number of icons for,
social media, RSS, etc. By default it only contains an RSS icon and link.

**info.html:** the info bar at the top of every page as a single `<aside/>`
element. This should probably be left alone but you can override it to remove
the info bar completely.

**meta.html:** empty partial included immediately after the meta tags.

**muc.html:** creates an `xmpp:` URI link to `.` with the query set to `?join`.

**nav.html:** the main navigation links in a single `<nav/>` element generated
from `.Site.Menus.main`; this should probably be left alone.

**phone.html:** prints `.telephone` or links it with a `tel:` URI if `.tel` is
specified.

**post-author-list.html:** creates a comma delimated list of author names for
the blog post footer.

**post-footer.html:** contains the blog post footer with tags, authors, and the
date in a single `<footer/>` element.

**post-tag-link.html:** generates a link to an individual tag page (`.` will be
the tag name).

**post-tag-list.html:** creates a comma delimited list of tag links for the blog
post footer by applying `post-tag-link.html` (`.` will be a slice of tag names).

### Shortcodes

**{{< email >}}:** executes the `email.html` partial with
`.Site.Params.contact.email`.

**{{< addr >}}:** executes the `addr.html` partial with `.Site.Params.contact`.

**{{< muc >}}:** executes the `muc.html` partial with
`.Site.Params.contact.muc`.

**{{< phone >}}:** executes the `phone.html` partial with
`.Site.Params.contact`.

**{{< icon name="icon-name" >}}:** inserts a [Fork Awesome] icon with the given
name (eg. `car` or `tree`).

**{{% hero caption="markdown" bgcolor="#000" height="80vh" img="background.jpg"
%}}Content{{% /hero %}}:** inserts a screen-width div with an optional
background color, cover image, caption, and content.

**{{% flex justify-content="" %}}Content{{% /flex %}}:** Used to put several
elements into a flex box.
Values for `justify-content` can be found on the [MDN article] about it.

Any shortcodes in the theme that are not documented here have not been finalized
and may be removed at any time without warning.

[Fork Awesome]: https://forkaweso.me/Fork-Awesome/
[MDN article]: https://developer.mozilla.org/en-US/docs/Web/CSS/justify-content


### Blocks

Your custom layouts that are based on `baseof.html` may define the following
blocks:

**main:** contains the `<main/>` element with the pages content by default.


## Submitting Patches

For information about development and submitting patches to this theme, see
[`CONTRIBUTING.md`].

[`CONTRIBUTING.md`]: https://git.sr.ht/~samwhited/co-op/tree/master/CONTRIBUTING.md


## License

Licensed under the BSD 2 Clause License ([LICENSE] or
https://opensource.org/licenses/BSD-2-Clause)

[LICENSE]: https://git.sr.ht/~samwhited/co-op/tree/master/LICENSE


### Contribution

Unless you explicitly state otherwise, any contribution intentionally submitted
for inclusion in the work by you shall be licensed as above, without any
additional terms or conditions.
