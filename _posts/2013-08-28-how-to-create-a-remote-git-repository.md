---
layout: post
title: How to create a remote Git repository
date: 2013-08-28 07:20:00
category: web
comments: true
---

This guide shows you how to create a remote Git repository on a server with SSH. 

#### The steps:

1. Connect to your server with SSH and create a directory for the new repository.
2. Write ``git --init bare repository.git`` in your shell.
3. Go to your local Git repository and write:  
``git remote add origin ssh://user@server/path/to/repo/repository.git``
4. Push to the server:  
``git push -u origin master``

That's it! 