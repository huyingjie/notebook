---
title: Content formatting
description: How to write content in a docs page and make it look nice.
---

This is the main page you should read before writing lots of documentation, since your life will be easier if you follow this stuff right away.

<h2 id="headings">Headings</h2>

One of the most important features of this docs framework is the automatic table of contents. This is powered by inspecting the `<h2>` and `<h3>` headings in the body text. These look like this:

```html
<h2 id="headings">Headings</h2>

<h3 id="why-html" title="Why HTML?">Why HTML and not markdown?</h3>
```

You probably have your first question...

<h3 id="why-html" title="Why HTML?">Why HTML and not markdown?</h3>

You'll notice that we *do not* use the regular markdown heading format, which looks like this:

```md
### Don't do this
```

There's two simple reasons: URL consistency and duplicate URLs. One of the best features of documentation is that you can link to it, and people really like being able to link to specific headings. If you use the default markdown approach above, you get a URL like:

```
formatting.html#Don%E2%80%99t-do-this
```

Not only is it ugly, but it depends on the exact text in the heading. If someone comes back and later changes that heading text to say something slightly different, the link won't work anymore. This is actually a huge problem for GitHub READMEs all over the place since people don't realize the issue.

Note that this heading style works just fine on GitHub, so we aren't breaking people's ability to read docs there by doing this.

<h3 id="picking-id">Picking an ID</h3>

Pick something that would look nice in a URL, and isn't overly specific in case we need to change that heading text later. Keep in mind that every ID in the docs is us committing to someone being able to link to that thing, broken links are the absolute worst.

<h3 id="heading-sidebar">Custom sidebar text</h3>

You may have noticed in the above example we also have a `title="..."` in the heading tag, like so:

```html
<h3 id="why-html" title="Why HTML?">Why HTML and not markdown?</h3>
```

What this does is let you separately pick the text that shows up in the sidebar. So the text in the `title` attribute will be displayed in the sidebar, while the content of the tag is displayed in the page. This can be useful if you have a heading that is too long to fit on one line in the sidebar.

<h3 id="h2-h3">Use H2 and H3</h3>

For the sidebar/table of contents to work properly, you need to have your headings be H2 and H3 headings nested in a logical fashion. H1, H4, and others are ignored by the table of contents logic (since H1 is in the [title](#title)).

<h3 id="sentence-case">Use sentence case</h3>

Headings just look better if you use sentence case. Avoid Capitalizing Every Word In The Heading, it looks overly formal.

<h2 id="title">Title and description</h2>

The title and description of a page is set using something called "YAML front matter". It looks something like this:

```
---
title: The Apollo and Meteor docs framework
description: Truly meta, this is the docs for the docs.
sidebar_title: Introduction
---
```

There are 3 properties supported by this docs framework, all represented above.

- *title:* The title that shows up at the top of the page. Used in the page `<title>` for SEO reasons.
- *description:* A subtitle that shows up below the title. Used in the page meta tags for SEO reasons.
- *sidebar_title:* Allows you to set a different title for this article in the sidebar vs. on the actual page, similar to `title` on headings. A common use case is to use something short like "introduction" for the sidebar, while having a more descriptive title on the page.

<h2 id="links">Links</h2>

Link to other parts of the same page [with a hash](#title):

```
[with a hash](#title)
```

Link to a different page with a relative URL with `.html` at the end. Note that the URLs have `.html` and not `.md`. For example:

```
[Some text with a link](./formatting.html)
```

You can combine both to link to a particular section of a different page:

```
[Some text with a link](./formatting.html#title)
```

<h3 id="backcompat">Link backcompat</h3>

You can insert "fake" headings for backwards compatibility reasons, for example if you removed a heading, by using an `<a>` tag with a `name` attribute, like so:

```
<a name="any-url-hash"></a>
```

<h2 id="images">Images</h2>

Add images by putting them somewhere in the `source/` folder next to your markdown, and putting a relative path. For example:

```
![Coffee](./coffee.jpg)
```

Makes:

![Coffee](./coffee.jpg)

<h2 id="tables">Arbitrary HTML</h2>

You can put arbitrary HTML anywhere you want in the middle of the markdown. For example, here's a YouTube embed:

```
<iframe width="560" height="315" src="https://www.youtube.com/embed/6ZfuNTqbHE8" frameborder="0" gesture="media" allow="encrypted-media" allowfullscreen></iframe>
```

Becomes:

<iframe width="560" height="315" src="https://www.youtube.com/embed/6ZfuNTqbHE8" frameborder="0" gesture="media" allow="encrypted-media" allowfullscreen></iframe>
