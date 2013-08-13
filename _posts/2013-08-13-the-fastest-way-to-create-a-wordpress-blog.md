---
layout: post
title: The fastest way to create a Wordpress blog
date: 2013-08-13 06:13:00
category: web
---

Yeah, I really think this is THE fastest way to create a new Wordpress project. You don't even have to leave Sublime.  

####Requirements:
 
*  [Sublime Text 2](http://www.sublimetext.com)
*  The "Nettuts+ Fetch" plugin for Sublime

####Setup:

1. Download the "Nettuts+ Fetch" plugin for Sublime
2. Press ``shift + commando + p`` and write ``Fetch:manage``
3. Add the following line to the packages array:  
``"wordpress": "https://wordpress.org/latest.zip"``

####The steps:

1. Create a new folder and drag it into Sublime.
2. Press ``shift + commando + p``and write ``Fetch:package``.
3. Select **wordpress**. 

A few seconds later, you will have a brand new installation of Wordpress in the selected directory.
