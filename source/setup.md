---
title: Setup from scratch
description: How to set up a new docs site in a repo.
---

We hope to make it much easier to set up a new docs site soon, but in the meanwhile you might want to ask someone who's done it before. Here's the full documentation for how to do it.

<h2 id="repo">Add files to the repo</h2>

Maybe get a coffee first.

1. Go to the folder where you want the docs. For example, you might want this to be inside `docs` inside your repo.

2. Make directories called `/source`, `/themes`, `/assets`, and `/public`

3. Copy in `/assets/theme-colors.less` with the following content:

    ```
    @color-primary: #22A699;
    ```

4. Add the theme as a submodule.

    ```bash
    git submodule add https://github.com/meteor/hexo-theme-meteor.git themes/meteor
    # Check out the apollo branch inside the submodule if you're on an Apollo site
    ```

5. Add a `.gitignore`:
    ```
    .DS_Store
    Thumbs.db
    db.json
    *.log
    node_modules/
    public/*
    !public/_redirects
    .deploy*/
    docs.json
    ```

6. Create a `_config.yml`, [copy](https://github.com/apollographql/community/blob/master/_config.yml) and adapt it. Here are the most important fields:

    1. `sidebar_categories` defines the sidebar, and the order of the pages. This has to be correct for the site to work at all.
    2. `github_repo` should be the name of your repo, like `apollographql/apollo-link`
    3. `content_root` should be the path to the directory where your *actual source markdown* is, like `docs/source`
    4. `url` should be the complete url, like `https://www.apollographql.com/docs/link/`
    5. `root` should be the part after the domain, like `/docs/link/`
    6. `public_dir` should be like root but with public, like `public/docs/link`

7. Create a `public/_redirects` file, which is just one line. This makes Netlify deploy previews easier to use since we aren't hosting the sites at the root of the domain.

    ```
    / /docs/your-url/
    ```

8. Copy in a package.json: <https://github.com/apollographql/community/blob/master/package.json>

9. Test it. Good luck!
    1. `npm install` inside the docs directory (commit `package-lock.json`)
    2. `npm start` to run the site (this should be a package script that has `hexo serve` in it)

<h3 id="common-errors">Common errors</h3>

```
Cannot read property 'title' of undefined
```

This means that the “page” is undefined, which means it can't find something in your `sidebar_categories`. Check if you have a page listed there which doesn't exist in your source directory.

<h2 id="netlify">Deploying to Netlify</h2>

We try to use netlify for our deploys because it gives you nice deploy previews on PRs, and makes it super easy to set up HTTPS.

1. Push to GitHub
2. Go to <https://app.netlify.com/teams/meteor/sites>. If you're not on the Netlify team called “meteor”, get someone to invite you. (this process will still work if you're not in the team, but it will be harder for others to manage the site)
3. Click “new site from git” and create a new site with the repository you pushed to
4. In build settings, put:
    1. If your site is at the root:
        1. Build command: `npm run build`
        2. Publish directory: `public`
    2. If your docs are in a subdir like docs, instead do:
        1. Build command: `cd docs && npm i && npm run build`
        2. Publish directory: `docs/public`
5. Don't forget to add the “meteor” team
6. Hit deploy!
7. Set a nice name for the site, instead of the auto-generated one.

<h2 id="routing">Adding to fly.io routing</h2>

This is for paths that are under <https://www.apollographql.com>.

1. Go to <https://fly.io/sites/www-apollodata-com/backends>
2. If you're not on the fly.io “meteor” team, ask someone to add you
3. “Add backend”
4. Select “Netlify” and then type in the name of your site (the thing that goes before “.netlify.com”)
5. **Do not** mount at path!
6. Go to “rules” in the sidebar
7. “Add routing rule”
8. In “Path to match” put your path, **without a trailing slash**. Make sure “prefix” is selected on the right.
9. Select the right backend
10. Click the button at the bottom to save
11. Set the priority to something reasonable, like a single digit number. It should be lower priority than the https redirect rule
12. Test going to apollographql.com/your-url-here!

<h3 id="routing-common-errors">Common errors</h3>

If you see “not found”, maybe your backend name doesn't match your Netlify site name. Fly.io doesn't check this for you at all.

