---
title: "blog.init()"
date: 2021-06-01T21:42:31+08:00
draft: false
---

This is a short write-up of how I got this blog up and running. There's a lot of
options available out there -- from ready-to-go blogging platforms to building
your own site with a static site generator -- I went with the latter option
using [Hugo](https://gohugo.io) and hosting it on [GitHub Pages](https://pages.github.com).

Being able to just write stuff in Markdown and not having to worry about styles
and layouts (my design skills leave much to be desired) were the main reasons
for going this route, not to mention the services you can use to host your blog
for free.

Time to get started.

##  Acquiring a domain name

Arguably the hardest and most time-consuming step, usually a lot of back and
forth going before you land on a domain name that you like and one that is
available.

You'll get one, eventually. :smile:

## Setting up a GitHub repo

The next step is setting up a GitHub repository that will house the content for
the site and will be hosted directly from said repo.

To get started, create a [new repo on Github](https://github.com/new) with the
name *username*.github.io, where *username* is your GitHub username i.e. 
*j4ckofalltrades*.

*If the first part of the repository doesn’t exactly match your username,
it won’t work, so make sure to get it right.*

## Linking your custom domain to GitHub Pages 

The actual configuration will vary based on the domain name registrar that you
used -- the following instructions are specific to [Namecheap](https://namecheap.com).

Basically the following records need to be added to the custom domain:

- `A` record for `@` pointing to 185.199.108.153
- `A` record for `@` pointing to 185.199.109.153
- `A` record for `@` pointing to 185.199.110.153
- `A` record for `@` pointing to 185.199.111.153
- `CNAME` record for `www` pointing to your *username*.github.io repo

The resulting config should look something like:

| Type | Host | Value |
|-|-|-|
| A | @ | 185.199.108.153 |
| A | @ | 185.199.109.153 |
| A | @ | 185.199.110.153 |
| A | @ | 185.199.111.153 |
| CNAME | www | *username*.github.io |

*Normally, it takes around 30 minutes for newly-created records to take effect.*

## Setting up Hugo

1. Install Hugo

   ```sh
   # on Linux distros with snapd support
   $ snap install hugo

   # on Debian or Ubuntu
   $ sudo apt-get install hugo

   # on Mac (using Homebrew)
   $ brew install hugo
   ```

2. Create new Hugo site and link to existing GitHub repo

   ```sh
   # replace username with your GitHub username
   $ hugo new site username.github.io
   $ cd username.github.io
   $ git init
   $ git remote add <link_to_repo>
   ```

3. Adding a theme

   There are tons to choose from at [Hugo Themes](https://themes.gohugo.io/),
   this site uses [Coder](https://themes.gohugo.io/hugo-coder/).

   ```sh
   # add theme as a submodule to the hugo website
   $ git submodule add https://github.com/luizdepra/hugo-coder.git themes/hugo-coder
   ```

4. Update site configuration

   Update `config.toml` using this [sample config](https://github.com/luizdepra/hugo-coder/wiki/Configurations#complete-example)
   as a guide.

5. Add some content and run site locally

   ```sh
   # create first post
   $ hugo new posts/first-post.md
   $ echo "Hello World" >> posts/hello-world.md
   
   # run site locally
   $ hugo serve
   ```

The site should now be accessible at [http://localhost:1313/](http://localhost:1313/).

## Setting up a publishing workflow with GitHub Actions

Once everything looks good locally, the last step is to push the changes to the
repo and publish the generated content. To automate the publish step, I used the 
[Hugo Setup Action](https://github.com/marketplace/actions/hugo-setup) and 
[GitHub Actions for GitHub Pages](https://github.com/marketplace/actions/github-pages-action#github-actions-for-github-pages)
actions.

Doing so is as simple as creating a `.github/workflows/gh-pages.yml` file in
your repo with the following content:

```yaml
name: github pages

on:
  push:
    branches:
      - main  # Set a branch to deploy

jobs:
  deploy:
    runs-on: ubuntu-18.04
    steps:
      - uses: actions/checkout@v2
        with:
          submodules: true  # Fetch Hugo themes (true OR recursive)
          fetch-depth: 0    # Fetch all history for .GitInfo and .Lastmod

      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: '0.77.0'
          extended: true

      - name: Build
        run: hugo --minify

      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public
          cname: <custom_domain> # your custom domain here
```

After you push your changes make sure to set the Source branch under your
repo's GitHub Pages settings to `gh-pages` (default or to whatever you set as
the `publish_branch` ) as this is where the generated content is published.

*Usually it takes a couple of hours for the DNS changes to propagate so don't
worry if your site isn't up yet. Just chill for a bit then press `F5` like a
madman to see check if it has completed.*

That's all there is to it, time to get blogging.