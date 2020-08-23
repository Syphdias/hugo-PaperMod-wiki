-   [Intro](#intro)
-   [Override theme template](#override-theme-template)
-   [Enable Social-Metadata and SEO](#enable-social-metadata-and-seo)
-   [Failed to find a valid digest in the 'integrity' attribute for resource ... ?](#failed-to-find-a-valid-digest-in-the-integrity-attribute-for-resource--)
-   [Archive Page](#archive-page)
-   [Bundling Custom css with theme's assets](#bundling-custom-css-with-themes-assets)
-   [Custom Head / Footer](#custom-head--footer)
-   [Add menu to site](#add-menu-to-site)
-   [Pin a Post](#pin-a-post)
-   [Adding Custom Favicon(s)](#adding-custom-favicons)
-   [Centering image in markdown](#centering-image-in-markdown)
-   [References](#references)

---

## Intro

-   **We'll be using `yml/yaml` format for all examples down below, I recommend using `yml` over `toml` as it is easier to read.**

-   You can find any [YML to TOML](https://www.google.com/search?q=yml+to+toml) converters if necessary.

---

## Override theme template

By Hugo's Lookup Order, you can override any part of a theme that you want. The following is a quick example.

Let's say you wish the `list` was different. All you have to do is copy the `list` template:

```shell
your-site/themes/papermod/layouts/_defaults/list.html
```

And paste it under your own `layouts` folder:

```shell
your-site/layouts/_defaults/list.html
```

Then you're free to make any changes you want to the `list`.
When Hugo builds your site, your copy of `list.html` will be used instead of the theme's `list.html`.

---

## Enable Social-Metadata and SEO

These include OpenGraph, Twitter Cards and Schema.

```yml
params:
    env: production
```

or set `HUGO_ENV` as "production" in system env-vars

---

## Failed to find a valid digest in the 'integrity' attribute for resource ... ?

Read about How Subresource Integrity helps: [Subresource_Integrity](https://developer.mozilla.org/en-US/docs/Web/Security/Subresource_Integrity)

Why was the `asset` not loading ? : [How_browsers_handle_Subresource_Integrity](https://developer.mozilla.org/en-US/docs/Web/Security/Subresource_Integrity#How_browsers_handle_Subresource_Integrity)

**Solution:**

Set the following in `config.yml`

```yml
params:
    assets:
        disableFingerprinting: true
```

Linked Issues:

-   https://stackoverflow.com/questions/65056585/hugo-theme-not-loading
-   https://stackoverflow.com/questions/65040931/hugo-failed-to-find-a-valid-digest-in-the-integrity-attribute-for-resource
-   https://blog.gerardbeckerleg.com/posts/hugo-failed-to-find-a-valid-digest-in-the-integrity-attribute-for-resource/

---

## Archive Page

```shell
.
├── config.yml
├── content/
│   ├── archives.md   <--- Create archive.md here
│   └── posts/
├── static/
└── themes/
    └── hugo-PaperMod/
```

and add the following to it

```yml
---
title: "Archive"
layout: "archives"
url: "/archives/"
summary: archives
---

```

---

## Bundling Custom css with theme's assets

-   For adding custom css to be bundled inside one minimized css

Create folder in yout project directory as

```
.(site root)
├── config.yml
├── content/
├── theme/hugo-PaperMod/
└── assets/
    └── css/
        └── extended/  <---
        │   ├── custom_css1.css <---
        │   └── any_name.css   <---
```

All `css` files inside `assets/css/extended` will be bundled !

**Note**: blank.css is just the placeholder so that it doesn't break the theme when no files are present under `assets/css/extended`

Linked Issues:

-   [Papermod Theme: How to add custom CSS?](https://discourse.gohugo.io/t/papermod-theme-how-to-add-custom-css/30165)

---

## Custom Head / Footer

Custom css/js can be added by way mentioned below.

```
.(site root)
├── config.yml
├── content/
├── theme/hugo-PaperMod/
└── layouts
    ├── partials
    │   ├── comments.html
    │   ├── extend_footer.html <---
    │   └── extend_head.html   <---
    └── robots.txt
```

Create a html page in directory structure as shown above.

Contents of `extend_head.html` will be added to `head` of page.

and contents of `extend_footer.html` will be added to bottom of page.

---

## Add menu to site

You can add menu entries which will appear in the header of every page.

To do so, add a `menu` section to your site's `config.yml`:

```yml
menu:
    main:
        - identifier: categories
          name: categories
          url: /categories/
          weight: 10
        - identifier: tags
          name: tags
          url: /tags/
          weight: 20
        - identifier: example
          name: example.org
          url: https://example.org
          weight: 30
```

`name` controls what will be displayed for the menu entry.
`url` sets the URL that the entry points to.
`weight` is used to control the positioning of entries.

For more information on menus, see the [Hugo wiki page](https://gohugo.io/content-management/menus/).

---

## Pin a Post

Post can be pinned/ displayed top on the list by adding a `weight=<num>` var to page-variables

example:

```yml
---
title: "My Important post"
date: 2020-09-15T11:30:03+00:00
weight: 1
---

```

```yml
---
title: "My 2nd Important post"
date: 2020-09-15T11:30:03+00:00
weight: 2
---

```

---

## Adding Custom Favicon(s)

We support the following paths under `/static` directory
and can be added accordingly.

-   `favicon.ico`
-   `favicon-16x16.png`
-   `favicon-32x32.png`
-   `apple-touch-icon.png`
-   `safari-pinned-tab.svg`

1. Favicon(s) can be generated by [Favicon.io](https://favicon.io)

    and can be simply put in `/static` folder.

2. Other way is to add favicon(s) NOT located in `/static` folder.

    In site config add the following:

    ```
    params:
    assets:
        favicon: "<link / absolute url>"
        favicon16x16:  "<link / absolute url>"
        favicon32x32:  "<link / absolute url>"
        apple_touch_icon:  "<link / absolute url>"
        safari_pinned_tab:  "<link / absolute url>"
    ```

    - `absolute url` means direct links to external resource: ex. https://web.site/someimage.png

    example:

    ```
    params:
    assets:
        favicon: "/favicon.ico"
        favicon16x16:  "/favicon-16x16.png"
        favicon32x32:  "/favicon-32x32.png"
        apple_touch_icon:  "/apple-touch-icon.png"
        safari_pinned_tab:  "/safari-pinned-tab.svg"
    ```

---

## Centering image in markdown

Add `#center` after image to center align an image

```md
![name](path/to/image.png#center)
```

---

## References

-   [Override a Hugo theme](https://zwbetz.com/override-a-hugo-theme/)