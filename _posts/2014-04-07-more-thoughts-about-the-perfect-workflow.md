---
layout: post
title: More thoughts about the perfect workflow
date:   2014-04-07 08.18.00
category: web
comments: true
---

In my previous post about Git workflows with Wordpress, I suggested that you should put all files, including plugins and core files, under version controll. For example, Chris Coyer does this in his [screencast](http://css-tricks.com/video-screencasts/109-getting-off-ftp-and-onto-git-deployment-with-beanstalk/) about this subject. 
However, I don't think it's the best way to work in every possible situation. For example, the state of the art PHP framework [Laravel](http://laravel.com) is a Composer package. Thus it will be stored in the ``vendor`` directory which is by default listed in the ``.gitignore`` file. So in the context of a Laravel project, all files except the framework itself and its dependencies are included in the Git repository. That would correspond to not include Wordpress or the required plugins in your repository. 
But Wordpress isn't Laravel and we don't have the fancy ``composer.json`` file around. We can't do ``composer install`` or ``composer update`` to get Wordpress and all the standard plugin that we always use installed. (Unless we use [Wordpress Packagist](http://wpackagist.org) which might be a good solution).  


One variant that I've seen has used Wordpress as a Git submodule. With that approach, you will have a pretty clean project root which after a bit of configuration could look like this:

````
index.php   
wp-config.php   
content/  
	themes/  
	plugins/  
	uploads/  
wp/   
	// Wordpress files.
	// You’ll never touch this folder
````

So when it's time to upgrade Wordpress to the latest version, you update the submodule and checkout the tag you wanna use. ``git checkout 3.8.1`` for example.  
I think this could be a pretty good solution, but as I said, it requires a bit of configuration in ``wp-config.php`` to make it find the Wordpress itself and the content directory. But remember, you need to have git installed on the production server to make this work.  

A similar approach that I learnd about this weekend is to put the ``wp-content/`` folder under version control. You'll ignore the ``uploads/`` folder of course, but your themes and plugins will be taken cared of by Git, which is most important.  
With [WP Migrate DB Pro](https://deliciousbrains.com/wp-migrate-db-pro/) you and your collegues can keep the local databases in sync with the production database.  

As you might have guessed, I've changed my mind about what should go into the Git repo and what shouldn't. But I still think that it all comes down to the specific project that you're working on just now.  
As a last disclaimer, this was just another post by me with my most recent thoughts about this very interesting but hard subject. So stop laughing at me and help me find **the** best and most elegant solution.  
Until then, here are a few good links:

- [Developing and deploying Wordpress](http://guides.beanstalkapp.com/deployments/deploying-wordpress.html)
- [Managing and deploying Wordpress with Git](http://blog.g-design.net/post/60019471157/managing-and-deploying-wordpress-with-git)
- [Collaborative Workflow for WordPress Development](https://deliciousbrains.com/collaborative-workflow-wordpress-development/)