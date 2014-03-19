---
layout: post
title: The (hunt for the) perfect Wordpress workflow
date:   2014-03-19 07:40:00
category: web
comments: true
---

Workflows and best practices are something that I am kind of obsessed about.  What's the best way to concatenate and minify scripts and stylesheets? To optimize images? To manage dependencies?  
When working with static files, [Yeoman](http://yeoman.io) is the best tool around I think. But how often do we have the pleasure to work with only static HTML files? With no server-side stuff involved at all? The answer is: almost never.  
Whenever there's somehing going on server-side, Wordpress is not far away. But hey, we all love Wordpress, don't we?  
I love WP, but I also love good wordflows. So what's the best workflow for a Wordpress project? Well, I've spent many, many hours researching the subject and trying to find the answer for that question. But the thing is that I still don't know the answer and I might never find it.  It's like the Kennedy assassination, we might never find out the truth.  
However, we can always have theories about what the best workflow is or if the CIA was involved or not.  
Regarding Wordpress, I've finally come up with a theory about what the perfect workflow looks like.

##Git
We all know that we should use a version control system and that usually means Git. Twitter has told us that Git is good and Subversion is bad and hard to learn.  
But what should we include into our Git repository? The theme or the whole Wordpress installation? Well, that's (also) a hard question and I think it depends on the situation. But in most cases I think that we should put the whole thing, except the ``uploads/`` directory, into version control. If John Doe installs a plugin, Jane Doe will also have it after the next ``git pull``.  
When it's time to upgrade Wordpress to the latest version, you could do that on your local installation and then push it up to the production server.  

###Collaborate
Okey, but if you're a part of a team who works on the project? How would that workflow look like?  
Well, you could have a repository for the project at [Github](http://www.github.com) which should be the center of the workflow. Nothing should be deployed to the production server before it has been merged with the Github repo.  
Let's pretend that John Doe starts working on a big, new feature on the site. He does a ``git pull`` from Github, thus ensureing that he's completley up to date with the code.  
John works on this new feature durning a couple of weeks and is ready to deploy it. However, meanwhile John has worked on the new feature, Jane Doe has made several bugfixes and deployed them. So before John kan push up the new feature, he has to do a ``git pull`` and merge his changes with Janes.  
In short:  

1. ``git pull``
2. Make your changes.
3. ``git pull`` from Github (might of course not be necessary all the time).
4. Resolve merge conflicts if there is any.
5. ``git push`` to Github
6. Deploy

##Deployment
FTP-based deployment is bad and Git-based is good. This is the truth and we all know it. But how can we switch? We might not have a fancy, dedicated server that we can do whatever we want with around all the time. Sometimes we have to stick with a cheap shared hosting environment. In that case, FTP is our only option.  
I find a tool called [Dploy](http://leanmeanfightingmachine.github.io/dploy/) to be a very good choise in those situations. It's built on Node.js and you'll be up and running with it very fast.  
After you've commited a change to Git and wants to deploy it, you only need to run ``dploy server_name`` and Dploy will upload the changes to the server. 'server_name' is of course a placeholder for the name of the server that you've set up in the configuration file.  
Like I said, I find this a very good and simple solution that will work with any server. Dploy makes it easy to move up from FTP-based deployment **today** .

##Database
This is (also) a tricky one. Exporting a Wordpress database requires a little bit of work since all permalink is hard coded and not relative.  
First, you need to export a dump of the database. Then you have to open it in an texteditor and do a search and replace for the old and new URL. ``localhost:8888/project`` should become ``project.com``.  Then you have to import the dump to the new database.  
This solution will do the job, but it's not optimal. I don't know what the best solution is, but I do have a theory about that to.  
[WP Migrate DB Pro](https://deliciousbrains.com/wp-migrate-db-pro/) is a one-click solution for keeping databases in sync.  
Let's say that Jane Doe are going to work on a site that she released a couple of months ago. Her local version of the site is way out of sync with the live version. The workflow would look like this:

1. ``git pull`` from Github in case John has made any changes to the site.
2. Download the data from the production database using the plugin.
3. Work on the site.
4. ``git push`` to Github.
5. ``dploy production`` (or to a testing server first, but you get the point).

Another good thing with WP Migrate DB Pro is that it also keeps the ``uploads/`` folder in sync. With the search and replace workflow, you would have to download that folder from the production server manually.  

##TL;DR
The perfect Wordpress development workflow might not even exist. The workflow in the 5K+ characters described above is definitly the best one. It's just a theory of how it could look like.  
Please, stop laughing at me and tell me your thoughts about the subject instead. Until then, Github, Dploy and WP Migrate DB Pro might be ingredients that could make a workflow that's not perfect, but is working. 