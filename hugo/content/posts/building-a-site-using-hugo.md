---
title: "Building a Site Using Hugo"
date: 2019-01-20
draft: false
---

I recently moved my blog to [Hugo](https://gohugo.io/) from [Jekyll](https://jekyllrb.com/). My main motivation was that previously having experience with other static site generators such as [Pelican](https://github.com/getpelican/pelican) and Jekyll, I wanted to give the newest one a try. Other reasons to try Hugo is that it's written in Golang which is supposed to be fast, and that I liked some of the Hugo themes I've seen.

If you're not familiar with static site generators, they serve as frameworks for building websites and blogs. All of your content is written in Markdown files, and the generator makes the rest of the site. It makes it easy to create a site or blog in minutes without having to fuss with the layout. It also makes it easy to switch to a new theme since all your contents are written in Markdown files.

Having gone through the process myself, I figured it would be a good idea to make (yet another) blog post about building a site using Hugo. Hopefully this tutorial will either help others to build their first site, migrate their old site to Hugo, or to help with any bugs or challenges they encounter.

## Downloading and Installing Hugo

Let's get started by downloading and installing Hugo. The latest version can be found [here](https://github.com/gohugoio/hugo/releases).

Hugo can also be installed via a package manager such as `brew` on Mac OS or `apt` on Ubuntu. However, in the processes of building my site, I discovered that certain themes are dependant on which version of Hugo you use. The versions maintained in these repositories might not be the latest release. Therefore, when looking at themes, take note of the version required and install the necessary version.

Once Hugo has been installed, we can verify the installation is successul by going to the terminal and running the following command:

```
$ hugo version
```

which will output the version of Hugo installed on your machine.

## Creating a New Project

As mentioned earlier, static blog generators provide frameworks to build a site. It creates all the files necessary to build your site. All you need to do is provide content.

To create a new Hugo project, run:

```
$ hugo new site [name of site]
```

where `[name of site]` is what you want to name your project. This command will create all the necessary directories and files required to build your site.

Moving into the project directory, we see the following files and directories:

```
archetypes/
config.toml
content/
data/
layouts/
static/
themes/
```

* `config.toml`: This is the configuration file for your site
* `content`: Markdown files for your content will go here
* `themes`: Directory to store your Hugo themes

## Installing a Theme

Currently Hugo does not have a default theme when creating a new project, therefore, we need to install one. You can browse different Hugo themes [here](https://themes.gohugo.io/). You are also free to install themes from other sources like [Reddit](https://www.reddit.com/r/gohugo/).

Once you have found a theme you like, you can clone it to the `themes` directory in your project. In order for your site to use the theme you downloaded, add the line to your `config.toml`:

```
theme="[name of theme]"
```

Most theme creators provide documentation and instructions on how to install and use their themes. Mainly, they provide a sample `config.toml` which you can copy to your project. To get your site up and running, we can start a local instance with the following command:

```
hugo server -D
```

Running this command will start a live instance of your website in debug mode. This means after making changes to your site, the changes are made in real time.

## Creating Content

Once your theme is installed and your site is set up, it's time to start writing posts.

Here's a [cheatsheet](https://gohugo.io/commands/) of other useful commands.

Once your site is ready, you can publish your site by running:

```
$ hugo
```

in the root of your project. This will create a new directory called `public/` which will contain all the files for your website.

Congratulations, your site is ready to be uploaded to GitHub Pages, or whatever service you use!

