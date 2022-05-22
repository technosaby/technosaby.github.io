---
layout: splash
title: "Jekyll Based Portfolio"
date: 2021-08-23 7:42
header:
  overlay_color: "#000"
  overlay_filter: "0.5"
  overlay_image: /assets/images/jekyll_image.png
excerpt: "Using jekyll to build portfolio"
tags:
  - Jekyll
  - config
  - portfolio
---

# Background
[Jekyll](https://jekyllrb.com/) is a nice way of converting plain text to static website and blogs. You can write the contents in [markdown](https://en.wikipedia.org/wiki/Markdown) and put a theme on top of that of make a nice portfolio or blog website. You can select any paid or free theme from [Jekyll themes](https://jekyllthemes.io/). For this portfolio, I have selected the Minimal Mistakes [Jekyll theme](https://jekyllthemes.io/theme/minimal-mistakes) theme.

# Installation  
There are many ways of installing the themes. Normally the theme documentation contains all the details. You can follow that at any day. 
The generic process 
1. Clone the repo from the Github repo, in my case it is [Minimal Mistakes](https://github.com/mmistakes/minimal-mistakes) 
2. Install all the dependencies. These can be well documented by theme developer in [many cases](https://github.com/mmistakes/minimal-mistakes). Otherwise run step 3 and resolve errors as you go.
3. Run the local server using the following command 
``` 
bundle exec jekyll serve
``` 
This will help you test your portfolio page on a local host.
4. Build the static pages using the following command 
``` 
bundle exec jekyll build
```
  
# Content
1. If you want to update the generic configutaions for the site which are common across all the screens(like theme, title, repository configuration, etc), the _config.yml file should be modified. 
2. For other content related changes with respect to posts, the post file should be created in the following format YYYY-MM-DD-file-name.md. (You can have separate format defined in the _config.yaml file as well). At the top of the file, you can define parameters like title,date etc in the [font matter](https://jekyllrb.com/docs/front-matter/). An example is given below.
```
---
layout: posts
title: "Jekyll Based Portfolio"
subtitle: "Here is some sub title"
date: 2021-08-23 7:42
tags:
  - Jekyll
  - config
  - portfolio
---
```
3. If you want to create a separate page like an About page, you can create a separate file (e.g. about.md) in the root dirctory and have a font matter at the top with the contents of the file
4. For defining the navigation, you can modify the _navigation.yaml file under the _data folder. A sample navigation font matter is as follows
```
main:
  - title: "Home"
    url: /
  - title: "ML Projects"
    url: /ml-projects/
  - title: "RL Projects"
    url: /rl-projects/
  - title: "Other Projects"
    url: /other-projects/
  - title: "Notes"
    url: /notes/
  - title: "Posts"
    url: /year-archive/
  - title: "About"
    url: /about/
```
5. If you tend to forget the markdown syntax, Please feel free to refer to the [markdown cheatsheet](https://guides.github.com/pdfs/markdown-cheatsheet-online.pdf).

# Host on Github
If you have a github account, you can create a public repo with *username.github.io*, where username is your username (or organization name) on GitHub. You can follow the detailed steps in this [Github link](https://pages.github.com/)

