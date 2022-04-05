---
title: "Test Render Link Render Hook"
date: 2021-10-17T10:14:26Z
publishDate: 2021-10-17T10:14:26Z
author: Daniel F. Dickinson
categories:
    - Demonstration
tags:
    - Links
    - Testing
---

## Test of render link render hook

<!--more-->

### Should work with both GitHub and Hugo

```markdown
[A test of a valid filename and a fragment (also go to accessibility goals)](../accessibility.md#goals)
```

[A test of a valid filename and a fragment (also go to accessibility goals)](../accessibility.md#goals)

```markdown
[A test of pointing to a parent directory of this page](..)
```

[A test of pointing to a parent directory of this page](..)

```markdown
[A test of pointing to a relative directory beside this page's parent directory](../docs)
```

[A test of pointing to a relative directory beside this page's parent directory](../docs)

```markdown
[Test of a bare (this page) fragment](#test-of-render-link-render-hook)
```

[Test of a bare (this page) fragment](#test-of-render-link-render-hook)

### Will only work with Hugo

```markdown
[Go to Accessibility Goals](../accessibility#goals)
```

[Go to Accessibility Goals](../accessibility#goals)

```markdown
[A test of pointing to an absolute directory](/post)
```

[A test of pointing to an absolute directory](/post)

```html
{{</* link-special href="/a-nonexistant-internal-link" destinationNoFind="true" */>}}A non-existant link that would error on build if 'destinationNoFind' was not true (will 404 if you follow it).{{\< /link-special >}}
```

{{< link-special href="/a-nonexistant-internal-link" destinationNoFind="true">}}A non-existant link that would error on build if 'destinationNoFind' was not true (will 404 if you follow it).{{< /link-special >}}

```html
{{</* link-special href="placeholder" wrapperElement="span" */>}}A link with a wrapper element.{{</* /link-special */>}}
```

{{< link-special href="placeholder" wrapperElement="span">}}A link with a wrapper element.{{< /link-special >}}
