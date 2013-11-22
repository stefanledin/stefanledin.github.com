---
layout: post
title:  "Git off FTP deployment!"
date:   2013-11-22 23:45:00
category: web
comments: true
---

So you've read about this Git thing on Twitter or maybe listened to an annoying colleague who keeps talking about it. Perhaps you've come to the conclusion that Git  is something good and you should probably use it.  
There is one problem though. You got Git installed on your local machine, but you are stuck on a shared hosting service that kinda sucks. You have no possibility to use Git for deployment like the *real* professionals seams to do. Until now!  
I've tried a ["Git powered FTP client written as a shell script"](https://github.com/git-ftp/git-ftp) that seams to work quite well.  
First, you need to have [Homebrew](http://brew.sh) (and Git of course) installed to get set up on Mac OS. When you got that installed you should be able to run `brew` from the command line.  
These are the commands you have to execute in order to install git-ftp:  

{% highlight php %}
brew install grep  
brew install git  
brew install curl --with-ssl --with-ssh  
brew install git-ftp  
{% endhighlight %}

The official guide for installation is [available here](https://github.com/git-ftp/git-ftp/blob/develop/INSTALL.md).  
Now it's time to try it out!

###Step 1
Create a new directory and cd into it.  
{% highlight php %}
mkdir test && cd $_  
{% endhighlight %}

###Step 2
Create a new file and write something random in it.  
{% highlight php %}
touch index.html 
{% endhighlight %}

###Step 3  
Create a new Git repository and commit the file.
{% highlight php %}
git init  
git add index.html  
git commit -m 'First commit'
{% endhighlight %}

###Step 4
Okey, now it's time to push the file to the server. 
{% highlight php %}
git ftp init -u exampleusername.com -p ftp://ftp.exampleserver.com/optionalsubdirectory  
{% endhighlight %}
Hit return and write the password for your server. index.html should have been uploaded now if everything went well. Congratulations!  

###Step 5
Make a random change in index.html and make a new commit.
{% highlight php %} 
git add index.html  
git commit -m 'Second commit'
{% endhighlight %}
But wait, you don't wanna write your credentials every time you're going to push changes to the server. Instead you can save them to the config file:
{% highlight php %}
git config git-ftp.user exampleusername.com
git config git-ftp.url ftp://ftp.exampleserver.com/optionalsubdirectory
git config git-ftp.password qwerty123
{% endhighlight %}
And you're ready to push the file to the server.
{% highlight php %}
git ftp push
{% endhighlight %}

###Step 6
Celebrate! You are now a real developer.

**return false;**
