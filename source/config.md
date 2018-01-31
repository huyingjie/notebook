---
title: _config.yml
description: An archaeological excursion into the depths of available configuration.
---

You may have heard we have a lot of sites running the same theme. How? Well, because we put a bunch of junk into the config, that's how! Neat. If you discover some new config options please add them here.

<h2 id="meta">Metadata</h2>

<h3 id="title">title</h3>

This is appended to the `<title>` of every page in the docs, so it will be something like `_config.yml | Docs docs`. It's also used at the top of the sidebar.

<h3 id="versions">versions</h3>

TODO: Document this. Used in Meteor docs/guide.

<h2 id="sidebar">sidebar_categories</h2>

Example:

```
sidebar_categories:
  null:
    - index
    - formatting
  Technical:
    - setup
    - recipes
    - config
```

This is what organizes all the pages into a sidebar. The top-level keys are the categories, allowing you to group pages into thematic categories.

The keys inside are the filenames, without `.md`. So for example, if you have a `source/formatting.md`, you should just put `formatting`. You can also use subdirectories, like `basics/queries`.

<h3 id="sidebar-external">External sidebar links</h3>

Recently we added a feature that allows the sidebar to link to other sites entirely by specifying a title and href:

```
sidebar_categories:
  null:
    - index
    - example
  Servers:
    - servers/express
    - servers/hapi
    - servers/koa
  Related:
    - title: graphql-tools
      href: https://www.apollographql.com/docs/graphql-tools/
    - title: GraphQL Subscriptions
      href: https://www.apollographql.com/docs/graphql-subscriptions/
```

<h2 id="social">Social / APIs</h2>

Use these to add various buttons/integrations/social stuff.

<h3 id="github-repo">GitHub</h3>

```
github_repo: apollographql/docs-docs
content_root: source
```

This is used to power the "Edit on GitHub" buttons on the pages. The repo is used to construct the GitHub URL, and the content root is when you have the content in a nested directory.

<h3 id="social-twitter">Twitter</h3>

```
social_links:
  twitter: '@apollographql'
```

Used for Tweets to identify us as the owner of the page.

<h3 id="social-slack">Slack</h3>

```
social_links:
  slackInvitePage: 'https://www.apollographql.com/#slack'
```

Adds a "Discuss on Slack" button to the pages with this URL.

<h3 id="segment">Segment</h3>

```
apis:
  segment: wgrIo8Bul0Ujl8USETG3DB6hONdy4kTg
```

Add segment analytics for page loads.

<h3 id="gtm">Google Tag Manager</h3>

```
apis:
  gtm: GTM-PNFDVBB
```

Add GTM to every page.

<h2 id="url">URLs</h2>

```
# URL
## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
url: https://www.apollographql.com/docs/docs/
root: /docs/docs/
```

<h2 id="source-dir">Source directory</h2>

TODO document this

```
# Directory
source_dir: source
public_dir: public/docs/docs
```

<h2 id="unused">Unused / broken</h2>

Please fix these, or remove them if you see them in a config file.

<h3 id="subtitle">subtitle</h3>

It's only used in the placeholder text in the search field.

<h3 id="description">description</h3>

Totally unused.
