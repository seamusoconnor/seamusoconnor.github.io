---
title: Migrating site from Raspberry Pi to GitHub pages
date: 2022-11-11 21:00:00 +0100
categories: [site]
tags: [github, coding, development]
---


## Background

Several years ago, I setup a simple blog to capture what technical stuff I was interested in at the time. I also wanted to get an understanding of web devlopment, how to deploy a website, and some coding. I looked at some web-hosting services but wanted to maintain my own hardware and see what came with that experience.

I bought a Raspberry PI B+, downloaded WordPress, and with some luck and a few long evenings, was able to get a self-hosted website going. I probably spent more time getting the website up and running than actually writing posts but it was good fun. 

The hardware was somewhat limited for what was running on it so eventually I got a RaspBerry Pi3 and migrated the site from one RPI to the other. It ended up being a challenge because outside of updating the site with a new post, what typically would happen is:

1. Something went wrong
2. I would realise I had no memory of how I set it up orginally
3. I would spend hours fixing some arcane issue ( like when the RPI would not boot fully if a keyboard was not attached on boot )
4. I would fix it
5. I would forget how I did it

this happened enough times that I moved the RPI from the attic to my office, not because the site broke often, but more because when it did, it wasn't possible for me to fix it remotely.

although WordPress is a nice, relatively simple to have a small blog, it was also a black box for me, and when I migrated form RPI B+ to RPI3, I spen da bunch of time migrating databases, which amounted to blindly copying files from one PI to another, hoping I would get enough data to figure out what was happening.


Additionally, over time I had added some other services to the RPI3, a piHole server, a PLEX media server and whatever technology at the time I was playing with. It meant that I had a bunch of services running that made me cautious of breaking something.


## What was I looking for

Ideally, I wanted to get out of the hardware side of the web-hosting, free up my RPI for more experimental purposes, while having a deploy-and-forget blog. Working on ambiguous technical issues for my day job, and whatever additional study I was doing meant spending two days trying to debug the Raspberry PI without breaking the site or some other forgotten tool, wasn't advancing my technical knowledge or reducing the friction of making new posts


My other requirement was to have some standard, plain-text-based, portable site so If there was complications with the platform, I could pull my content and at least move to something else.

I had checked hosting on AWS/Google Cloud but altough they have static website hosting, it just seemed I would be adding some unneeded overhead.

The other promising option was hosting through Notion but I explored it and for whatever reason I can't think of now, it was a non-runner.

## Moving to GitHub

GitHub Pages, through Jekyll,  ticked all the boxes so I spent about an hour researching and was able to deploy the site following a nice tutorial on youTube. The simplicity, and ability to use Markdown and Git makes it portable ( and understandable ) for me. Getting the site up and running was really easy and if it does have major issues that I haven't been exposed to, It looks simple to just pull my posts and go somewhere else.


## How to deploy your site GitHub Pages with Jekyll

I followed this  <a href="https://www.youtube.com/watch?v=F8iOU1ci19Q" target="_blank">YouTube</a>  video from  <a href="https://www.youtube.com/c/TechnoTimLive" target="_blank">Techno Tim</a>

and the Jekyll  <a href="https://jekyllrb.com/docs/installation/macos/" target="_blank">documentation</a>

I'm using an Intel Mac, VSCode and have a free GitHub account.

I followed the guide <a href="https://jekyllrb.com/docs/installation/macos/" target="_blank">here</a>
Istalled HomeBrew, the non-system Ruby they mentioned, and also used the theme mentioned in the YouTube video.

I have a GitHub account but the GitHub pages part of it I took directly from the YouTube video.

Once everything was installed locally, I was able to run the basic site locally with

```bash

bundle exec jekyll serve

```
which spins up a webserver on on: ```127.0.0.1:4000/```

Deploying to GitHub Pages, I there's a CI/CD pipeline that runs, which in basic terms, builds the site for the platform its going to run on and deploys it to that server. I got a build failure with a helpful <a href="https://github.com/seamusoconnor/seamusoconnor.github.io/actions/runs/3349608580/jobs/5549782019#step:4:34" target="_blank">message</a>   

which gave me a helpful message

```log
  Your bundle only supports platforms ["x86_64-darwin-21"] but your local platform
  is x86_64-linux. Add the current platform to the lockfile with
  `bundle lock --add-platform x86_64-linux` and try again.
  Took   0.73 seconds
```

so I added x86_64-linux to my Gemfile.lock file.
``` 
PLATFORMS
  x86_64-darwin-21
  x86_64-linux
```

In a way, the way this error was presented, gives me confidence that this is a product which has good support.


For adding posts, you can use the file structure here, just create a new .md file and start writing

![Posts](/assets/images/2022-11-11-migrate-to-github/posts1.png)

and do a git add and commit and push changes to your site. You can use Git to track changes and reverting them if needed should be the same as with any Git file.



### DNS

To migrate the site off the Raspberry PI, I changed by A and CNAME DNS to point to GitHub's IP addresses and my GitHub Pages site name, and the change was pretty quick and painless - I used this <a href="https://www.youtube.com/watch?v=EX4w9hsduNA" target="_blank">YouTube</a> Video  as a guide 


### Conclusion

Moving to GitHub Pages, with Jekyll has been a simple process with clearly explained steps, has less complications than running your own hardware and feels like once it is setup, gets out of your way to allow you to write with minimal friction.



