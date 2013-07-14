---
layout: post
title: "Moved to Github Pages and Octopress"
date: 2013-06-29 17:26
comments: true
categories: 
---

<h3>29 June 2013</h3>

So, I was bored again with my current blogging framework and decided to move to Github Pages. I've made a couple of research and Octopress is apparently the way to go and is based on Jekyll. So how does one setup a Github Pages site with Octopress? 

If you don't have a Github account, do it!

1. Create a repository with $YOUR_USERNAME_OR_ORGANIZATION.github.io
2. Install git, ruby, bundle and rake. 
3. Make sure that your ruby version is 1.9.3. I'm currently using RVM.
4. `git clone git://github.com/imathis/octopress.git octopress`
5. `cd octopress`
6. `bundle install`
7. `rake install`
8. `rake setup_github_pages` and enter your repository details
9. Make sure that origin points to your local repository. You can double check with `git remote -v`
10. Modify your _config.yml file
11. `rake generate`
12. `rake deploy`
13. Wait for a couple of minutes and your blog will be up on yourdomain.github.io
14. To change your theme, go to the [Octopress Themes](https://github.com/imathis/octopress/wiki/3rd-Party-Octopress-Themes) page and follow the instructions.
15. Once you're done for the day, don't forget to commit and push your changes with `git push origin source`