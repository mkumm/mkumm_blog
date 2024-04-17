+++
title = 'Up and Running With Hugo'
date = 2024-04-15T12:40:00+01:00
tags = ['go', 'dev', 'blog', 'hugo', 'blowfish']
draft = false
+++

This post is mostly about getting [Hugo](https://gohugo.io/) and [Blowfish](https://blowfish.page/) up and running and published to [Fly.io](https://fly.io/). Feel free to jump to [Hugo Quickstart](#hugo-quick-start) to skip the backstory.

## Backstory

### Motivation

I have been using Elixir/Phoenix/Nimble for my blog posts for the last couple of years. It was okay, but I felt I was spending too much time tweaking the code and not enough time creating content. Additionally, I did not find the experience of creating new content pleasant - whatever that means.

I decided to take a look around and see what was availabel these days. So so many options. I decided to put together a little wishlist.

### My Wishlist

I want to...

- use a platform that I didn't have to think about once I set it up.
- write in [markdown](https://daringfireball.net/projects/markdown/syntax).
- own my content and maybe cross post to other platforms.
- use my own domain.
- have some creative control but start with something sensible.
- enjoy creating content again (again, whatever that means).
- make it easier to quickly be helpful to others.
- maybe learn some different tech.

### Considerations

I looked at Ghost, Medium, Squarespace, Dev.to, and several other platforms that 'just let me start posting.' What they were selling just wasn't valuable to me. I didn't want to automatically collect emails, or monetize my blog. I wasn't looking to build an audience (that I actively monitor), etc.

I did spend about an hour considering writing my own static site generator (maybe in C) but eventually decided that I didn't want so shave a yack before I started blogging (maybe later). My search led me to static site generators which brought me to the usual players: Gatsby, Jekyll, Hugo and I tried them all.

### Hugo For the Win!

Hugo was fast. I am really, really fast. Rendering was in the sub-second range with a few posts. Hugo also had a nice collection of starter templates (I chose Blowfish) and in pretty short time I had a working prototype of what my blog would be. Super happy with Hugo and Blofish.

The rest of this post is sharing some things I learned while setting up and publishing this blog.

## Hugo Quick Start

The following is how I set up and configured Hugo with Blowfish.

### My starting environment
I am using a Mac (Apple Silicon) with homebrew, git, node, and GO. If you don't have these installed yet, you will need to do that. Follow the install directions - probably start with [homebrew](https://brew.sh/).

### Install Hugo and Blowfish

There are a lot of options when choosing how to install Hugo and Blowfish, the following worked well for my quick setup and I did not run into any problems later in the process.

```console
$ brew install hugo
```

Navigate to whereever you want to setup your blog on your local system and run the following commands. Replace `blog-name` with the name of your blog. I used `mkumm-blog`.

```console
# from ~/Dev
$ hugo new site blog-name

$ cd blog-name
```

```console
# from ~/Dev/blog-name
$ git init

$ git submodule add -b main https://github.com/nunocoracao/blowfish.git themes/blowfish
```

I ignored all of the Blowfish install tools and any alternative methods of installation. Using the submodule option puts you in a good place later on.

### Add Your Basic Config

Now there is one more thing to do before we can see our local development site. We need to copy our `blog-name/themes/blowfish/config` directory to the root of our project and make one small edit to one of the files.

```console
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
    	└── config # copy this directory
    		└── _default
```

```console
$ cp -r themes/blowfish/config .
```

```console
├── archetypes
├── assets
├── content
└── config # directory just added
    └── _default
├── data
├── hugo.toml
├── i18n
├── layouts
├── public
├── static
└── themes
```

Now for that one small edit. Open up `blog-name/config/_default.hugo.toml` and uncomment line 5 so the start of the file looks like this.

```toml
# editing blog-name/config/_default/hugo.toml

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

After saving `blog-name/config/_default/hugo.toml` you can run the following...

```console
# from ~/Dev/blog-name/

$ hugo server
```

and then take a look at [localhost:1313](http://localhost:1313) in your browser.

![hugo start page](image1.png)

### Thing We Did

By adding the Blowfish git submodule to our system, we ended up with a sub-directory called `themes/blowfish`. Do not edit files directly in the `themes/blowfish/` directory.

When Hugo is looking for the files it needs, it will first look in _your_ files, which is pretty much everything but your themes directory. If it can't find the file it needs, it will then lookup that file in your configured theme. You can think of your theme as basically your default source for all files.

When we ran the command `hugo server` we asked Hugo to launch a basic webserver, dynamically generate the static files it needs and then server them on port 1313. As you might imagine, there are a lot of options available - well documented on the [Hugo Documentation Site - Hugo server](https://gohugo.io/commands/hugo_server/). **Spoilers** To actaully build your site for production, the command is even shorter `hugo`.

And that's all it takes to set up a bare bones Hugo Server with a custom  themes. Let's create our first blog post.

## First Blog Post

In the documentation you will see there are many options for how you can set up your files for blog posts. To get started, let's keep it simple and leave enough flexibility for later.

### Hello World

Let's use Hugo's built in generators to give us a markdown file with helpful front matter. That is just a fancy way of asking Hugo to set up a new post for us.

```console
$ hugo new content posts/hello_world/index.md
```

This will create a new directory `content/posts/hello-world/index.md` with a markdown file which we will use to create our first blog post.

```text
# content/posts/hello-world/index.md

+++
title = 'Hello_world'
date = 2024-04-15T22:20:02+02:00
draft = true
+++
```

The text between the two `+++`s is our _front matter_ which is not directly visible in our post. Let's edit this file so we can see our post in a browser. By default, Hugo will not show posts with `draft = true`

```text
# content/posts/hello-world/index.md

+++
title = 'Hello World'
date = 2024-04-15T22:20:02+02:00
draft = true
+++

## Hello World!

We are here!
```

We edited our _front matter_ to give us a human looking title and changed draft from `true` to `false` as well as adding the obligatory "Hello World!" text. Once we save the file we can see our post added to our list of posts (which of course just has one at the moment): [localhost:1313/posts/](http://localhost:1313/posts/)

![image2](image2.png)

You can view the entire post by clicking on the listing. [localhost:1313/posts/hello_world](http://localhost:1313/posts/hello_world)

![image3](image3.png)

Looks great, but if we are starting from the home page, we will never find our posts. Let's fix that.

### Add "Blog" To Site Menu

Let's make one last edit so we have a link on our homepage to our posts. Uncomment lines 13-16 in `config/_default/menus.en.toml` so it looks like this

```toml
# -- Main Menu --
# The main menu is displayed in the header at the top of the page.
# Acceptable parameters are name, pageRef, page, url, title, weight.
#
# The simplest menu configuration is to provide:
#   name = The name to be displayed for this menu link
#   pageRef = The identifier of the page or section to link to
#
# By default the menu is ordered alphabetically. This can be
# overridden by providing a weight value. The menu will then be
# ordered by weight from lowest to highest.

[[main]]
 name = "Blog"
 pageRef = "posts"
 weight = 10

#[[main]]
#  name = "Parent"
#  weight = 2
.
.
```

We are telling Hugo to add "Blog" to our navigation and have it point to our "posts" content folder. When you save the above file click into your homepage, you should see the following:

 [homepage!](http://localhost:1313)

### Thing We Did

We used the Hugo generator to create a directory for our blog post and add an index.md which is the markdown file we edit to write our post. Technically we don't need to create a directory for every post, but with a directory we can add images, video, whatever to the directory and we can reference those files conveniently with a little markdown `![image1](image1.png)`.

We edited our `config/_default/menus.en.toml` file to start to build out our navigation. If you explore that file (and other toml files) you see start to see how much control we have just by editing configuration.

Now is a good time to start exploring the sample blowfish site in `themes/blowfish/exampleSite` for inspiration on what is easily possible. By the way that example site is already up and running - it's the same one used on
[Blowfish Website](https://blowfish.page/)

I am hoping you have enough information to start developing your blog on Hugo/Blowfish. The next section will cover building your static site and how to push your blog on [fly.io](https://fly.io) (other examples are well documented on the [Hugo site](https://gohugo.io/hosting-and-deployment/)).

## Build and Deployment

So far we have updated some configuration files, added a theme, and temporarily rendered our content to view on our local browser. The next step will create a "permanent for now" version of our static site, which is all we really need to share with the world. To build our site we have to enter the following.

### Build

```console
$ hugo
```

Yep, that's it. Our `public/` directory is now populated with everything you will need (and at the moment more) to deploy your site publicly.

### Prep for Deployment

Hugo's `hugo deploy` with some minimal configuration can be used to deploy to all the regular players and it is a great option. What is not well documented is setting up a more generic deployment using Docker and a provider like [fly.io](https://fly.io) - which is the provider I have been using for the last year or so.

**Set up a Docker File**

Create a new file named `Docker`

```console
# from blog-name

$ touch Docker
```

Edit Docker file so the entire file looks like this

```txt
FROM pierrezemb/gostatic
COPY ./public/ /srv/http/
```

**Just for fun**

You can now run this docker file locally but feel free to move right to [Time to Fly.io](#time-to-fly.io)

Assuming you have docker on your local system.

```console
# from ~/Dev/blog-name/
$ docker build -t myblog .
```

Once built, you can launch your blog with

```console
$ docker run -d -p 8043:80 myblog
```

Because the server we chose uses port 8043, we just needed to map all of our localhost (port 80) requests to the docker server's port 8043.

Now you can go to your [localhost](http://localhost) and see your full static site as it will be deployed.

### Time to Fly.io

**Set up Fly.io cli tools**

If you don't have an account yet, go to [fly.io/docs/hands-on/install-flyctl/](https://fly.io/docs/hands-on/install-flyctl/) to set up `flyctl` and follow the first two steps. (I have no affiliation and receive no incentives from Fly.io).

Once you have installed `flyctl` and created your account, deployment is 2 steps away.

**Create your fly.toml file**

We are going to let flyctl create this for us.

```console
$ flyctl launch
```

You will be asked two questions, just answer 'N' in both cases
_Do you want to 'tweak' these settings?_. **N**
_Do you want to add dockerignore...?_. **N**

Fly will continue to deploy your site, but it won't actually work yet. Let's update that `fly.toml` that was just created for us.

```toml
1 # fly.toml app configuration file generated for blog-name on 2024-04-17T11:43:28+02:00
┆   2 #
┆   3 # See https://fly.io/docs/reference/configuration/ for information about how to use this file.
┆   4 #
┆   5
┆   6 app = 'blog-name'
┆   7 primary_region = 'waw'
┆   8
┆   9 [build]
┆  10
┆  11 [http_service]
┆  12 ▏ internal_port = 8080
┆  13 ▏ force_https = true
┆  14 ▏ auto_stop_machines = true
┆  15 ▏ auto_start_machines = true
┆  16 ▏ min_machines_running = 0
┆  17 ▏ processes = ['app']
┆  18
┆  19 [[vm]]
┆  20 ▏ memory = '1gb'
┆  21 ▏ cpu_kind = 'shared'
┆  22 ▏ cpus = 1
```

We need to update our internal port from "8080" to "8043" so it looks like this

```toml
┆  11 [http_service]
┆  12 ▏ internal_port = 8043
┆  13 ▏ force_https = true
┆  14 ▏ auto_stop_machines = true
┆  15 ▏ auto_start_machines = true
┆  16 ▏ min_machines_running = 0
┆  17 ▏ processes = ['app']
```

No we can run

```console
$ flyctl deploy
```

and after some behind the scenes magic, follow the link it provides to view your newly published site! 🎉

![image4](image4.png)

### Destroy App

Fly.io let's you use up to $5 of resources for free each month so our new blog probably won't cost us anything, but there probably is no reason to keep this running.

Go to your [Fly.io Dashboard](https://fly.io/dashboard) and click on your new App. If this is your first time using Fly, it will be the only App listed.

![image6](image6.png)

Then scroll to the bottom of the page and click "Settings", this will give you the option to "Delete app"

![image7](image7.png)

And after a confirmation step, your app has been deleted.

## Next Steps

### Configuration

Get to know your `config/_default` files learn how much you can modify on your site before you add any design elements

[https://blowfish.page/docs/getting-started/](https://blowfish.page/docs/getting-started/)

### Add Some Style

Get some inspiration from the [Blowfish Samples page](https://blowfish.page/examples/) and then start playing around with different layouts [https://blowfish.page/docs/homepage-layout/](https://blowfish.page/docs/homepage-layout/)

### Configure TailwindCss to Reload on Change

Sadly you don't start with access to everything that TailwindCSS has to offer. Basically if a Tailwind code is currently being used in your site, you won't be able to see the changes you want until you "rebuild your css". To do this during development you will need to do 2 things.

1. Install the Tailwind compiler

```console
$ cd themes/blowfish
# and then from themes/blowfish run
$ npm install
```

Running this command will give you access to tailwind's tools which you will need to rebuild your css.

```console
# Get back to the root of your site
$ cd ../..
# and then run
$ ./themes/blowfish/node_modules/tailwindcss/lib/cli.js -c ./themes/blowfish/tailwind.config.js -i ./themes/blowfish/assets/css/main.css -o ./assets/css/compiled/main.css --jit -w
```
This second command will start a watcher on your site and will update your CSS whenever you make a change that requires it.

### Add General Pages (Contact, etc)

Take a look at the Blowfish [content-examples](https://blowfish.page/docs/content-examples/) to learn how to add pages that are not blog posts to your site.

## Feedback

I hope you found this post helpful. Feel free to [DM on Twitter @mkumm](https://twitter.com/mkumm) with any feedback or questions.
