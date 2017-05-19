To continue development on this small static application:

Ensure you have Hugo installed locally, clone this app into your Sites directory by running
  $ git clone git@github.com:SelenaSmall/hugo-selena.git

Start the server and browse to localhost:1313
  $ hugo server


---------------------------------------------------------
HERES HOW I BUILT THIS EXAMPLE AND DEPLOYED IT ON NETLIFY
---------------------------------------------------------

GO HUGO
————————————————————— 
Download and generate and new site
Go path already configured, simply download the generator with homebrew:
$ brew update && brew install hugo

In your Sites directory, generate a new site:
$ hugo new site <site_name>

Add a theme to your project by moving into he theme directory and cloning hugo’s robust theme:
$ git clone https://github.com/tomanistor/osprey.git
http://themes.gohugo.io/osprey/

Move into your new site’s root directory and generate some content - this theme allows for the generation of a new post:
$ hugo new blog/post-title.md

And also, the generation of a new portfolio entry:
$ hugo new gallery/image-title.md

Be sure to configure this new file and ensure the image you have linked to is available in your static/images path

Run hugo’s built in server form the root directory, ensuring the theme and buildDrafts flags are specified:
$ hugo server —theme=osprey —buildDrafts

  The above —buildDrafts flag specifies that articles are currently draft versions and not public. To make these **publicly available, simply updraft the content:
  $ hugo updraft content/post/good-to-great.md
  Then, you can start the server without in the buildDrafts option:
  $ hugo server —theme=osprey

————————————————————— 
Configure your Osprey theme
Update your config.toml options as per the instructions in the theme’s directory, in particular ensuring that you include the theme:
title = "Osprey Example Site"
baseURL = "https://tomanistor.com"
tags = ["portfolio", "web design", "blog"]
languageCode = "en-US"
config = "config.toml"
theme = "osprey"
canonifyURLS = true
googleAnalytics = ""

[Params]
    author = "Toma Nistor"
    description = "Full-stack web developer and UI/UX enthusiast based in San Diego, CA."
    logoBig = "/images/osprey-logo.png"
    logoSmall = "/images/osprey-logo.png"
    favicon = "favicon.ico"
    opengraphImage = "/images/osprey.png"
    twitter = "TomaNistor"
    linkedin = "tomanistor"
    github = "tomanistor"
    email = ""
    googleTagManger = ""
    highlightJS = true
    copyright = true
    credit = true

[[menu.main]]
    name = "Work"
    url  = "/#work"
    weight = 1
[[menu.main]]
    name = "Blog"
    url  = "/#blog"
    weight = 2
[[menu.main]]
    name = "Contact"
    url  = "/#contact"
    weight = 3

If it worked, you should be able to run the default server:
$ hugo server

You can now view your new Hugo site by directing your browser to the following address:
localhost:1313

————————————————————— 
Store site on GitHub
Create a new repo on Github
$ git init
$ git add —all
$ git commit -m ‘first commit’
$ git add remote origin <origin>
$ git push -u master

————————————————————— 
Git Modules
Create a .gitmodules file like this:
$ touch .gitmodules

And add your theme in there:
$ git submodule add https://github.com/tomanistor/osprey.git

It should look like this:
[submodule "themes/osprey"]
path = themes/osprey
url = https://github.com/tomanistor/osprey.git


Create a netlify configuration file in your project root called netlify.toml and add the Hugo version to your production environment context as follows:
[context.production.environment]
  HUGO_VERSION = "0.20"



————————————————————— 
Deploy site on Netlify
Sign up with Netlify if you haven't already done so at:
https://www.netlify.com/

Create a new project and configure your deploy settings for continuous deployment:
Repository: GitHub repo
Branch: master
Build Command: hugo
Publish Directory: public
