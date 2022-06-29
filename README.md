# DFD Hugo Link Handling

Hugo module with partials and shortcodes for improved link handling, including GitHub compatibility (page-relative links)

## Status

![build-and-verify](https://github.com/danielfdickinson/link-handling-mod-hugo-dfd/actions/workflows/build-and-verify.yml/badge.svg)

## GitHub Repository

<https://github.com/danielfdickinson/link-handling-mod-hugo-dfd>

## Features

* Handles \<a href="…"> links and \<link …> links.
* GitHub-compatible Markdown links (e.g. [A file in the same directory]\(``a-file-in-the-same-directory``) will work).
* We default to adding only "noopener" to \<a href="…"> links.
* We do provide a simple mechanism for link only 'untrusted' links ("nofollow noreferrer noopener).
* We don't (by default) use target="_blank" on external links for reasons described in <https://www.wildtechgarden.ca/blog/accessible-design-no-blank/>.
* Avoids allowing arbitrary HTML (which reduces the opportunites for malicious content contributors to insert malicious code).
* Allows opening the link tag without closing in this module for more complex links (e.g. not just text). (Obviously the tag still needs to be closed, but this leaves the details up to you).
* Full control over generated links when using shortcode, pretty good control of Markdown links through params.
* Optionally auto-add a wrapper element around the link.
* Errors build on missing destinations for internal links (prevent internal 404 errors), with some caveats.
* Avoids creating anchors (\<a>) without an ``href``.

## Basic Module Use

### Importing the Module

1. The first step to making use of this module is to add it to your site or theme.  In your configuration file:
   ``config.toml``

   ```toml
   [module]
     [[module.imports]]
       path = "github.com/danielfdickinson/link-handling-mod-hugo-dfd"
   ```

   OR
   ``config.yaml``

   ```yaml
   module:
     imports:
       - path: github.com/danielfdickinson/link-handling-mod-hugo-dfd
   ```

2. Execute

   ```bash
   hugo mod get github.com/danielfdickinson/link-handling-mod-hugo-dfd
   hugo mod tidy
   ```

## Using the Layouts/Shortcode

### Common For All Links Handled By This Module

#### Params Controlling Link Finding/Output

All params may be set at the site or per-page level.

| Param | Default | Description |
|-------|---------|-------------|
| linkWrapperDefault | _(none)_ | Element to wrap around link element. Default for non-Markdown is no wrapper. For Markdown see the [Using Markdown Links](#using-markdown-links) section. |
| linkDefaultRel | "noopener" | Default "rel=" for any link created by this module. |
| linkLinkDefaultRel | _(none)_ | Override default "rel=" for \<link> elements. Default it to drop the "noopener" since it doesn't apply to \<link> elements. |

#### Using Markdown Links

Mostly you'll do this without thinking about it as the defaults will make sense. There are options for when you need them however.

##### Special Case

As a special feature for markdown such as []\(``https://example.com``) (that is a link with no text), add ``"nofollow noreferrer noopener"``. This provides an easy way to add 'untrusted' external links.

If you need text and untrusted links, you will need the "link-special" shortcode.

##### Params to Modify Markdown Links

All params may be set at the site or per-page level.

| Param | Default | Description |
|-------|---------|-------------|
| linkDefaultRelMarkdown | _(none*)_ | Default "rel=" for Markdown links is no setting (meaning the same as any link from this module, which is "noopener"). _Note_: As mentioned in the [Special Case](#special-case) section links with no text get "nofollow noreferrer noopener" by default. |
| linkDefaultNoFindMarkdown | _(none)_ | If set to true, skip checking if internal links exist and/or finding resources. **NB** This means, if true, that links page resources in a page bundle will _not_ be found for Markdown links. |
| linkWrapperElement | span | By default wrap Markdown links in span elements. Using "none" for this will omit the wrapper element. **NOTE** Replacing this by div can cause validation errors as often links in Markdown end up inside paragraph \<p> elements and div inside p is not allowed. |
| wrapperClass | "link-wrapper-demo-site" | Default "class=" for the wrapper element around the link (e.g. default span, per above). It is recommended to set this in your config as suits your CSS. |
| linkClassMarkdown | "link-markdown-demo-site" | Default "class=" for the actual link created from the Markdown. It is recommended to set this in your config as suits your CSS. |

### Use the "link-special" Shortcode

#### Basic Use of the "link-special" Shortcode

**NB** You can't mix positional (unnamed) parameters with named parameters, so the first two examples will only work when the only parameter is a the destination.

``{{\< link-special "/path/to/an/internal/destination" >}}link text{{\< /link-special >}}`` (external destinations are also valid).

OR

``{{\< link-special "/path/to/an/internal/destination" />}}`` (external destinations are also valid).

OR

``{{\< link-special href="/path/to/an/internal/destination" >}}link text{{\< /link-special >}}`` (external destinations are also valid).

OR

``{{\< link-special href="/path/to/an/internal/destination" />}}`` (external destinations are also valid).

#### Other Parameters for the Shortcode

| Shortcode Param | Default | Description |
|-----------------|---------|-------------|
| title | _(none)_ | "title=" attribute |
| rel | _(none)_ | "rel=" attribute (see above for default for all links) |
| target | _(none)_ | "target=" attribute |
| linkElement | _(none)_ | a or link — tag for link. Default is an 'anchor' (\<a href="…">) tag through the default for all links |
| linkClass | _(none)_ | "class=" attribute for link itself |
| wrapperElement | _(none)_ | Element for optional wrapper |
| wrapperClass | _(none)_ | "class=" element for optional wrapper |
| destinationNoFind | false | Whether to omit checking for existence of destination and/or checking for destination as a resource |

## Contributions welcome

[Our current TODO/FIXME items](https://github.com/danielfdickinson/link-handling-mod-hugo-dfd/issues?q=is%3Aissue+is%3Aopen+label%3Aenhancement)
[Items further filtered by 'good first issue'](https://github.com/danielfdickinson/link-handling-mod-hugo-dfd/issues?q=is%3Aissue+is%3Aopen+label%3Aenhancement+label%3A%22good+first+issue%22)

### Contributions not noted in source code

* TODO: #31 Can we enable some checking / getting links from resources on taxonomy / term pages?
* TODO: #32 Refactor partials directory structure to use self-explanatory dir names
* TODO: #33 Have a real test regime for the various features and expected behaviours, and get to 70% coverage
* REVIEW: #34 Maybe integrate with 'image-handling' module and (possibly) keep this module for the href/src/finding parts.
