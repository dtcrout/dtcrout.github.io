---
author: Darshan Crout
title: "Building a Site Using Hugo"
date: 2019-01-27
draft: false
---

As of late, I've been getting interested in software philosophies such as the [Unix philosophy](https://en.wikipedia.org/wiki/Unix_philosophy) and [Suckless](https://suckless.org/), hoping that they will provide me with some guidance on how to become a better programmer. I've also been wanting to redo my personal blog for quite some time, but never did because I would always get bogged down on choosing a theme. While browsing for site themes, I came across [Simple Hugo Theme](https://themes.gohugo.io/simple-hugo-theme/) which is a [Hugo](https://gohugo.io/) theme inspired by http://bettermotherfuckingwebsite.com/. If you're familiar with Suckless, *bettermotherfuckingwebsite* is piece of satire on how modern websites should be designed. Inspired, I decided I should approach my site from a simplicity standpoint and just focus on the content rather than the design. In the process of building it, I learned how to use Hugo.

For those who are not familiar with static site generators such as Hugo, they serve as frameworks for building websites and blogs. All of your content is written in Markdown files, and the generator makes the rest of the site. It makes it easy to create a site or blog in minutes without having to fuss with the layout. It also makes it easy to switch to a new theme since all your contents are written in Markdown files.

For those who are already familiar with Suckless, you're probably wondering why am I using Hugo? Site generators are most likely not Suckless... Well for one, I like the idea of static site generators as the content is independent of the site, since you write everything in Markdown. I also have experience with other site generators in the past such as [Pelican](https://github.com/getpelican/pelican) and [Jekyll](https://jekyllrb.com/) and I wanted to give Hugo a try. Compared to Jekyll which I used to build my previous site, Hugo is written in Golang which is faster than Ruby, and requires less dependencies to get your site up and running. So while Hugo might not be Suckless, I think of it as a step in the right direction while I better understand the philosophy.

So why write this post? Having gone through the process myself, I figured it would be a good idea to make (yet another) blog post about building a site using Hugo. Hopefully this tutorial will either help others to build their first site, migrate their old site to Hugo, or to help with any bugs or challenges they encounter.

## Downloading and Installing Hugo

Let's get started by downloading and installing Hugo. The latest version can be found [here](https://github.com/gohugoio/hugo/releases).

Hugo can also be installed via a package manager such as `brew` on Mac OS or `apt` on Ubuntu. However, in the processes of building my site, I discovered that certain themes are dependant on which version of Hugo you use. The versions maintained in these repositories might not be the latest release. So when looking at themes, take note of the version required and install the necessary version.

Once Hugo has been installed, we can verify the installation is successul by going to the terminal and running the following command:

```bash
$ hugo version
```

which will output the version of Hugo installed on your machine.

## Creating a New Project

As mentioned earlier, static blog generators provide frameworks to build a site. It creates all the files necessary to build your site. All you need to do is provide content.

To create a new Hugo project, run:

```bash
$ hugo new site [name of site]
```

where `[name of site]` is what you want to name your project. This command will create all the necessary directories and files required to build your site.

Moving into the project directory, we see the following files and directories:

* `config.toml`
  * This is the configuration file for your site. Changes you want to make to the layout, or things you want to add like links to social media will be added here
* `content/`
  * Directory for your site content. Markdown files for your content will go here
* `themes/`
  * Directory to store your Hugo themes

## Installing a Theme

Currently Hugo does not have a default theme when creating a new project, therefore we need to install one. You can browse different Hugo themes [here](https://themes.gohugo.io/). You are also free to install themes from other sources like [r/gohugo](https://www.reddit.com/r/gohugo/).

Once you have found a theme you like, you can clone it to the `themes` directory in your project. In order for your site to use the theme you downloaded, add the line to your `config.toml`:

```toml
theme="[name of theme]"
```

Most theme creators provide documentation and instructions on how to install and use their themes. Mainly, they provide a sample `config.toml` which you can copy to your project. To get your site up and running, we can start a local instance with the following command:

```bash
$ hugo server -D
```

Running this command will start a live instance of your website in debug mode. This means after making changes to your site and saving them, the changes are updated on the site in real time.

## Creating Content

Once your theme is installed and your site is set up, it's time to start writing posts. Again it helps to read the instructions on the theme you coose to use as it may require your Markdown files to be in particular directories. Typically, all content is stored in the `content/` directory. If you are making a blog, your blog posts will go in a separate folder called `posts/` which is in the `content/` directory.

To create a new post, run:

```bash
$ hugo new [name of post].md
```

where `[name of post]` is the name of your post. This will create a new Markdown file in the `content/` directory which you can then start editing.

If you're going to have code snippets in your posts, Hugo uses [Chroma](https://github.com/alecthomas/chroma) for syntax highlighting and is configured in your `config.toml` file. More information about syntax highlighting can be found [here](https://gohugo.io/content-management/syntax-highlighting/).

Furthermore, here's a [cheatsheet](https://gohugo.io/commands/) of other useful commands that might be helpful when creating content.

Once your site is ready, you can publish your site by running:

```bash
$ hugo
```

in the root of your project. This will create a new directory called `public/` which will contain all the files for your website. I'm using [GitHub Pages](https://pages.github.com/) for my site so publish my site, I simply pushed the contents of the `public/` directory into my site repository.

If you want to learn more, [Hugo's documentation](https://gohugo.io/documentation/) is great and recommended if you would like to how to better tune your site and content.

---

**[ Feb 26, 2019 ] Update:** I have found a new love with [Hugo Theme Basic](https://github.com/siegerts/hugo-theme-basic). I think it still gets the point of simplicity across. It was also easy to transfer the theme over which demonstrates the power of Hugo.
