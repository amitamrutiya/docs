---
title: Contributing to Docs
weight: 10
description: A detailed contribution guide for Layer5 Docs.
aliases:
  - /meshmap/reference/contributing-to-docs
---
## Contributing to the docs.layer5.io Website

Welcome to the GitHub repository for Layer5's documentation website!

The docs website is hosted at <https://docs.layer5.io>.

We use [Hugo](https://gohugo.io/) with the [google/docsy](https://github.com/google/docsy) theme for styling and site structure, and [Netlify](https://www.netlify.com/) to manage the deployment of the site.

## Quickstart

Here's a quick guide to updating the docs:

1. Fork the [layer5io/docs repository](https://github.com/layer5io/docs) on GitHub.

2. Make your changes and send a pull request (PR).

3. If you're not yet ready for a review, add "WIP" to the PR name to indicate it's a work in progress.

4. Wait for the automated PR workflow to do some checks.
   When it's ready, you should see a comment like this: `deploy/netlify — Deploy preview ready!`

5. Click **Details** to the right of "Deploy preview ready" to see a preview of your updates.

6. Continue updating your doc and pushing your changes until you're happy with the content.

7. When you're ready for a review, add a comment to the PR, remove any holds or "WIP" markers, and assign a reviewer/approver. See the [Layer5 contributor guide](https://layer5.io/community/handbook/contribution).

If you need more help with the GitHub workflow, follow  this [guide to a standard GitHub workflow](https://github.com/layer5io/docs/blob/master/CONTRIBUTING-gitflow.md).

## Local development

This section will show you how to develop the website locally, by running a local Hugo server.

### Install Hugo

To install Hugo, follow the [instructions for your system type](https://gohugo.io/getting-started/installing/).

**NOTE:** we recommend that you use Hugo version `v0.140.2`, as this is currently the version we deploy to Netlify.

For example, using homebrew to install hugo on macOS or linux:

```bash
# WARNING: this may install a newer version than `v0.140.2`
brew install hugo
```

### Install Node Packages

If you plan to make changes to the site styling, you need to install some **node libraries** as well.
(See the [Docsy setup guide](https://www.docsy.dev/docs/getting-started/#install-postcss) for more information)

You can install the same versions we use in Netlify (defined in `package.json`) with the following command:

```bash
npm install -D
```

### Run local hugo server

Follow the usual GitHub workflow of forking the repository on GitHub and then cloning your fork to your local machine.

1. **Fork** the [layer5io/docs repository](https://github.com/layer5io/docs) in the GitHub UI.

2. Clone your fork locally:

    ```bash
    git clone git@github.com:<your-github-username>/docs.git
    cd website/
    ```

3. Initialize the Docsy submodule:

    ```bash
    git submodule update --init --recursive
    ```

4. Install Docsy dependencies:

    ```bash
    # NOTE: ensure you have node 18 installed
    (cd themes/docsy/ && npm install)
    ```

5. Start your local Hugo server:

    ```bash
    hugo server -D
    ```

6. You can access your website at [http://localhost:1313/](http://localhost:1313/)

### Useful docs

* [User guide for the Docsy theme](https://www.docsy.dev/docs/getting-started/)
* [Hugo installation guide](https://gohugo.io/getting-started/installing/)
* [Hugo basic usage](https://gohugo.io/getting-started/usage/)
* [Hugo site directory structure](https://gohugo.io/getting-started/directory-structure/)
* [hugo server reference](https://gohugo.io/commands/hugo_server/)

## Menu structure

The site theme has one Hugo menu (`main`), which defines the top navigation bar. You can find and adjust the definition
of the menu in the [site configuration file](https://github.com/layer5io/docs/blob/master/hugo.toml).

The left-hand navigation panel is defined by the directory structure under the [`content/en` directory](https://github.com/layer5io/docs/tree/master/content/en).

A `weight` property in the _front matter_ of each page determines the position of the page relative to the others in the same directory.
The lower the weight, the earlier the page appears in the section.

Here is an example `_index.md` file:

```md
+++
title = "Getting Started with Layer5"
description = "Overview"
weight = 1
+++
```

## Docsy Theme

We use the [Docsy](https://www.docsy.dev/) theme for the website.
The theme files are managed with a [git submodule](https://git-scm.com/book/en/v2/Git-Tools-Submodules) in the `themes/docsy` directory.

**Do not change these files**, they are not actually inside this repo, but are part of the [google/docsy](https://github.com/google/docsy) repo.

To update referenced docsy commit, run the following command at the root of the repo:

```bash
# for example, to update docsy to v0.6.0
# WARNING: updating the docsy version will require you to update our overrides
#          check under: `layouts/partials` and `assets/scss`
git -C themes/docsy fetch --tags
git -C themes/docsy checkout tags/v0.6.0
```

## Documentation style guide

For guidance on writing effective documentation, see
the style guide for the Layer5 docs.

## Styling your content

The theme holds its styles in the [`assets/scss` directory](https://github.com/layer5io/docs/tree/master/assets/scss).

**Do not change these files**, they are not actually inside this repo, but are part of the [google/docsy](https://github.com/google/docsy) repo.

You can override the default styles and add new ones:

* In general, put your files in the project directory structure under `website` rather than in the theme directory.
  Use the same file name as the theme does, and put the file in the same relative position.
  Hugo looks first at the file in the main project directories, if present, then at the files under the theme directory.
  For example, the Layer5 website's [`layouts/partials/navbar.html`](https://github.com/layer5io/docs/blob/master/layouts/partials/navbar.html)
  overrides the theme's [`layouts/partials/navbar.html`](https://github.com/layer5io/docs/blob/master/themes/docsy/layouts/partials/navbar.html)

* You can update the Layer5 website's project variables in the [`_variables_project.scss` file](https://github.com/layer5io/docs/blob/master/assets/scss/_variables_project.scss).
  Values in that file override the [Docsy variables](https://github.com/layer5io/docs/blob/master/themes/docsy/assets/scss/_variables.scss).
  You can also use `_variables_project.scss` to specify your own values for any of the default [Bootstrap 4 variables](https://getbootstrap.com/docs/4.0/getting-started/theming/).

* Custom styles [`_styles_project` file](https://github.com/layer5io/docs/blob/master/assets/scss/_styles_project.scss)

Styling of images:

* To see some examples of styled images, take a look at the OAuth setup page in the Layer5 docs.
  Search for `.png` in the [page source](https://raw.githubusercontent.com/layer5io/docs/master/content/en/docs/gke/deploy/oauth-setup.md).

* For more help, see the guide to
  [Bootstrap image styling](https://getbootstrap.com/docs/4.0/content/images/).

* Also see the Bootstrap utilities, such as
  [borders](https://getbootstrap.com/docs/4.0/utilities/borders/).

The site's [front page](https://docs.layer5.io/):

* See the [page source](<https://github.com/layer5io/docs/blob/master/content/en/>.

* The CSS styles are in the [project variables file](https://github.com/layer5io/docs/blob/master/assets/scss/_variables_project.scss).

* The page uses the [cover block](https://www.docsy.dev/docs/adding-content/shortcodes/#blocks-cover) defined by the theme.

* The page also uses the [linkdown block](https://www.docsy.dev/docs/adding-content/shortcodes/#blocks-link-down).

## Using Hugo shortcodes

Sometimes it's useful to define a snippet of information in one place and reuse it wherever we need it.
For example, we want to be able to refer to the minimum version of various frameworks/libraries throughout the docs,
without causing a maintenance nightmare.

For this purpose, we use Hugo's "shortcodes".
Shortcodes are similar to Django variables. You define a shortcode in a file, then use a specific markup
to invoke the shortcode in the docs. That markup is replaced by the content of the shortcode file when the page is built.

To create a shortcode:

1. Add an HTML file in the `/docs/layouts/shortcodes/` directory.
   The file name must be short and meaningful, as it determines the shortcode you and others use in the docs.

2. For the file content, add the text and HTML markup that should replace the shortcode markup when the web page is built.

To use a shortcode in a document, wrap the name of the shortcode in braces and percent signs like this:

```code
  { {% shortcode-name %}}
```

The shortcode name is the file name minus the `.html` file extension.

**Example:** The following shortcode defines the minimum required version of Kubernetes:

* File name of the shortcode:

  ```
  kubernetes-min-version.html
  ```

* Content of the shortcode:

  ```
  1.8
  ```

* Usage in a document:

  ```
  You need Kubernetes version 1.28 or later.
  ```

Useful Hugo docs:

* [Shortcode templates](https://gohugo.io/templates/shortcode-templates/)
* [Shortcodes](https://gohugo.io/content-management/shortcodes/)

## Versioning of the docs

For each stable release, we create a new branch for the relevant documentation.
For example, the documentation for the v0.2 stable release is maintained in the [v0.2-branch](https://github.com/layer5io/docs/tree/v0.2-branch).
Each branch has a corresponding Netlify website that automatically syncs each merged PR.

The versioned sites follow this convention:

* `docs.layer5.io` always points to the current _master branch_
* `master.docs.layer5.io` always points to GitHub head
* `vXXX-YYY.docs.layer5.io` points to the release at vXXX.YYY-branch

We also hook up each version to the dropdown on the website menu bar.
For information on how to update the website to a new version, see the [Layer5 release guide](https://github.com/layer5io/docs/blob/master/docs_dev/releasing.md#releasing-a-new-version-of-the-website).

Whenever any documents reference any source code, you should use the version shortcode in the links, like so:

```
https://github.com/layer5io/docs/blob/master/scripts/gke/deploy.sh
```

This ensures that all the links in a versioned webpage point to the correct branch.
