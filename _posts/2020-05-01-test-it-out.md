---
title: About this blog
date: 2020-05-01 00:47:00 + 0800
categories:
  - Tips
author_staff_member: fae
image: /assets/white.png
large_header: false
---

### About the Blog.

I spent the last day and a half trying to build and polish this website. I came across a few annoying problems, and I think maybe I can share them with you guys. Also you can always email me if you have any questions about the usage of the template.

#### Categories

This is really annoying. The category folder that jekyll built, which is inside the '_sites' folder, can't be located by github server. It tends to regard the root of the project as 'site.baseurl', which is insane! In that case, the category page is always 404 on github server. 

I just don't have the money to use another server. So I pretend to solve this problem by manually moving the category folder to the root. That will do it, but every time I post something new or did some modifications, I have to take that extra step.

**Somebody, please help me here.**

#### Visits Counting

To count the visits, I use the javascript script written by **busuanzi**,  instructed by [this guy](https://www.dazhuanlan.com/2019/12/05/5de7f1780d67f/). So there is an extra 'js' folder in my repo. Yes, I learned some basic javascript, very basic.  So you can see a little footnote under every page.

F.Y.I., I didn't count the visits of every post because they are unstable, as mentioned above. 

#### Others

Before all that, when I started to build this site, I spent a whole night decorating it and run it on my local server. It can only be run by the line 'bundle exec jekyll ...'  The setup of bundle needs to work on things like Gemfile or something like that. That's kind of annoying. 

Also it wasn't until I came across the category problem did I actually realize, that local server is basically to change the website **url** into a local host, and the **baseurl** remains. I thought I solved the category problem by setting the baseurl as 'shanemankiw.github.io', yet it failed. It's a fatal problem of github! 

#### A Reminder

Just a reminder to y'all, I am completely in love with this template but there are a lot of problems with it. Just be careful. 

Also a reminder for myself: the steps I need to take to have a post:

1.  Write a markdown.
2. Add the post head to the markdown with time and categories and other stuff. Rename it and put it in '_posts'.
3. Delete the category folder outside.
4. bundle exec jekyll build
5. Copy the inside category folder outside.
6. git add .
7. git commit -m "a new post"
8. git push origin master