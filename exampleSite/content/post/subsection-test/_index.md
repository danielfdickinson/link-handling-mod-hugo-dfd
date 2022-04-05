---
title: "Post Subsection"
date: 2022-03-27T05:15:49Z
publishDate: 2022-03-27T05:15:49Z
author:
categories:
    - Uncategorized
tags:
    - Untagged
---

## Test of link hooks on section page

### Should work with both GitHub and Hugo

```markdown
[A test of a valid filename and a fragment (also go to accessibility goals)](../../accessibility.md#goals)
```

[A test of a valid filename and a fragment (also go to accessibility goals)](../../accessibility.md#goals)

```markdown
[A test of pointing to a parent directory of this section](..)
```

[A test of pointing to a parent directory of this _section_](..)

```markdown
[A test of pointing to a relative directory beside this page's parent directory](../../docs)
```

[A test of pointing to a relative directory beside this page's parent directory](../../docs)

```markdown
[Test of a bare (this page) fragment](#test-of-link-hooks-on-section-page)
```

[Test of a bare (this page) fragment](#test-of-link-hooks-on-section-page)

### Will only work with Hugo

```markdown
[Go to Accessibility Goals](../../accessibility#goals)
```

[Go to Accessibility Goals](../../accessibility#goals)

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
