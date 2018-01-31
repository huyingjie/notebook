---
title: Recipes
description: How to do some oddly specific things.
---

If you come across some cool idea, throw it in here!

<h2 id="moving-commits">Moving commits between repos</h2>

This has been useful to migrate docs between repositories without losing git history and credit for contributors.

```bash
# in source repo
# this line is needed if you are splitting a single doc repo into multiple
git filter-branch -f —subdirectory-filter tools/graphql-tools
# this moves the docs repo into a docs/source folder to prep it to move to the source repo
git filter-branch -f —tree-filter 'mkdir -p docs && mv * docs || true'

# in target repo
git fetch ../tools-docs/
git merge —allow-unrelated FETCH_HEAD
```
