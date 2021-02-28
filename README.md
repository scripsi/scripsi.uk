# scripsi.uk

This is the [scripsi.uk](http://scripsi.uk) website development repository.

The website content is written in Markdown and compiled to a static website with [MkDocs](https://www.mkdocs.org/) and the [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/) theme. A GitHub Action compiles and deploys the website to hosting.

This file just reminds me how things are configured and what to do to run the site.

## Developing content

From the root of a local copy of the repository run:

``` shell
mkdocs serve
```

Open a web browser to [http://127.0.0.1:8000](http://127.0.0.1:8000)

Add and edit markdown files in the `docs/` folder and use the browser to view the changes.

A local copy of the website can be built for testing in the `site/` folder:

``` shell
mkdocs build
```

 The `site/` folder is excluded from the repository in `.gitignore` so that it doesn't get uploaded to GitHub in a `git push`.

## Committing content

``` shell
git add .
git commit -m "commit message"
git push
```

## Github Action

The website is compiled and copied to the web hosting by a GitHub Action.

The action is configured in `.github/workflows/deploy-to-hosting.yml`
