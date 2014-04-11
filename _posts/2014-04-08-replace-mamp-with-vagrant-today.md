---
layout: post
title: Replace MAMP with Vagrant today
date: 2014-04-08 08.00.00
category: web
comments: true
---

Durning the last couple of months I've played around quite a bit with Vagrant. I'm sure that you've heard about Vagrant and understood that it's some new, cool thing that everybody should use.  
You may also have read that [MAMP](http://www.mamp.info) is bad and Vagrant is good, and now you've came across a little guide on how to replace MAMP with Vagrant.  
I'll be using the excellent [Vaprobash](https://github.com/fideloper/Vaprobash) script to the Vagrant server up and running.
##Installation
If you don't have [Virtualbox](http://www.virtualbox.org/) and [Vagrant](http://www.vagrantup.com/downloads.html) installed on your computer, go ahead and do that first!  

1. Create a new directory somewhere on your computer. That will correspond to what previously been your ``htdocs`` folder.
2. Download Vaprobash using the terminal. ``curl -L http://bit.ly/vaprobash > Vagrantfile``
3. Open the Vagrantfile and uncomment the lines where Apache and MySQL are getting installed. At the time of this writing, it's line 125 and 140.
4. Run ``vagrant up`` and wait for everything to get downloaded and installed. (This might take a while).

Okey, so now you have the virtual machine up and running. Success!  
Remember how you used to browse to ``http://localhost:8888/project1`` when using MAMP? Now when you are using Vagrant, the URL to your projects are ``http://192.168.33.10.xip.io/project1``. 

##Vhosts
First things first. Working with virtual hosts is very easy with MAMP Pro. It's not quite as fast and easy to set up vhosts with Vagrant, but it's not that terrible either.  
With that said, here's how you create a vhost called ``project1.dev`` 

1. Login to the server: ``vagrant ssh``
2. Add the name of the vhost and the path: ``sudo vhost -s project1.dev -d /vagrant/project1``
3. Exit out of the server: ``exit``
4. Edit the host file using Vim or your editor of choise: ``sudo vim /etc/hosts``
5. Add the following line: ``192.168.33.10   project1.dev``
6. Save the file and browse to ``http://project1.dev``

##Sequel Pro
Now let's connect to MySQL using Sequel Pro. At the connection screen, select the SSH tab and use these credentials:

- MySQL Host: ``127.0.0.1``
- Username: ``root``
- Password: ``root``
- SSH Host: ``127.0.0.1``
- SSH User: ``vagrant``
- SSH Key: `~/.vagrant.d/insecure_private_key`` (Click on the key icon and browse to that directory)
- SSH Port: ``2222``

Now you should be able to connect to the MySQL database inside the Vagrant server. 

##Last thoughts
This was a very quick and simple guide on how to get started with Vagrant. There's of course a lot more to learn about the subject, but I leave that research for you to do.  
The good thing about Vagrant is that you can fairly easy set up a local environment that is more or less the same as the production, which of course is something good. It can also be used to make sure that you the team you're a part of have exactly the same environment.  
However, I still think that it's completely fine to continue using MAMP. It will still do the trick in most projects and Vagrant might be overkill. But when the day comes when you have to deal with a production server using Nginx instead of Apache, give Vagrant a shot. 

