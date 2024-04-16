+++
title = 'Up and Running With HUGO'
date = 2024-04-15T12:40:00+01:00
tags = ['go', 'dev', 'blog', 'hugo', 'blowfish']
draft = false
+++

This post is mostly about my getting Hugo and Blowfish up and running. Feel free to jump to [Hugo Quickstart](#hugo-quick-start)

## Backstory

### Motivation

I have been using Elixir/Phoenix/Nimble for my blog posts for the last couple of years. It was okay, but I felt I was spending too much time tweaking the code and not enough time creating content. Additionally, I did not find the experience of creating new content pleasant - whatever that means.

Once I realized that I was open to using anything, I started to put together a list of "wants."

### New Blog Requirements

I want to...

- use a platform that I didn't have to think about once I set it up.
- write in markdown.
- own my content and maybe cross post to other platforms.
- use my own domain.
- have some creative control.
- enjoy creating content again (again, whatever that means).
- make it easier to share some things that might be helpful to others.
- be open to some different tech.

### Considerations

I looked at Ghost, Medium, Squarespace, Dev.to, and several other 'just start posting' platforms. I don't mind spending money for value, and I suggest that most platforms offer enough value for what they are selling, these things just were not valuable to me. I didn't want to automatically collect emails, or monetize my blog. I wasn't looking to build an audience (that I actively monitor).

I did spend about an hour considering writing my own static site generator (maybe in C) but eventually decided that this project didn't need any yack shaving. I did eventually start looking at static site generators which brought me to the usual players: Gatsby, Jekyll, Hugo and I tried them all.

### HUGO for the win

Hugo was fast. Really fast. To render my sample site with a few posts in development mode, the edits I made were rendered in sub-one-second time. Hugo also had a nice collection of starter templates (I chose Blowfish) and in pretty short time I had a working prototype of what my blog would be. Super happy with HUGO.

The rest of this post is sharing my setup, configuration, and hosting story.

## Hugo Quick Start

The following is how I set up and configured Hugo with Blowfish.

### My starting environment
I am using a Mac (Apple Silicon) with git, node, and homebrew. I am pretty sure I had GO installed already. 

### Install Hugo and Blowfish

There are a lot of options when choosing how to install HUGO and Blowfish, the following worked well for quick setup and being able to maintain the installs. 

```bash
$ brew install hugo
```

Navigate to where ever you want to setup your blog on your local system and run the following commands. Replace `<blog-name>` with the name of your blog. I used `mkumm-blog`. 
 


```bash
# from ~/Dev
$ hugo new site <blog-name>

$ cd <blog-name>
```

```bash
# from ~/Dev/<blog-name>
$ git init

$ git submodule add -b main https://github.com/nunocoracao/blowfish.git themes/blowfish
```

I ignored all of the Blowfish install tools and any alternative methods of installation. Using the submodule puts you in a good place later on for updates, etc.

### Add Your Basic Config

Now there is one more thing to do before we can see our local development site. We need to copy our `<blog-name>/themes/blowfish/config/_default` directory to the root of our project and make one small edit. 

```bash
├── archetypes
├── assets
├── content
├── data
├── hugo.toml
├── i18n
├── layouts
├── public
├── static
└── themes
    └── blowfish
    	└── config
    		└── _default # this dir
```

```bash
├── archetypes
├── assets
├── content
└── config # you just added this
    └── _default 
├── data
├── hugo.toml
├── i18n
├── layouts
├── public
├── static
└── themes
```

Now for that one small edit. Open up `<blog-name>/config/_default.hugo.toml` and uncomment line 5 so the start of the file looks like this.

```toml
# editing <blog-name>/config/_default/hugo.toml

# -- Site Configuration --
# Refer to the theme docs for more details about each of these parameters.
# https://blowfish.page/docs/getting-started/

theme = "blowfish"
# baseURL = "https://your_domain.com/"
defaultContentLanguage = "en"
.
.
.
```

### Launch Your Local Server

After saving `<blog-name>/config/_default/hugo.toml` you can run the following...

```bash
# from ~/Dev/<blog-name>/

$ hugo server
```

and then take a look at [localhost:1313](http://localhost:1313) in your browser.

![hugo start page](image1.png)

### Thing We Did 

By adding the Blowfish git submodule to our system, we ended up with a sub-directory called `themes/blowfish`. Do not edit files directly in the `themes/blowfish/` directory. 

When we copied over the `config/` directory and made that small edit, we basically told HUGO to look in the `themes/blowfish` directory **IF** HUGO can't find the file or directory it needs to build our site. In many cases we will want to copy files from our theme into our main system.

When we ran the command `hugo server` we asked hugo to launch a basic webserver, dynamically generate the static files it needs and then server them on port 1313. As you might imagine, there are a lot of options available - well documented on the [HUGO Documentation Site - hugo server](https://gohugo.io/commands/hugo_server/). **Spoilers** To actaully build your site for production, the command is even shorter `hugo`.

And that's all it takes to set up a bare bones Hugo Server with a custom themes. In the next section I will go over setting up our first blog post.

## First Blog Post









### Updating TailwindCSS after changes


## Push To Production

## Learnings
