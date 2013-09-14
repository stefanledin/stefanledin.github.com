---
layout: post
title: "For dummies: A local environment in Laravel 4"
date: 2013-09-13 16:10:00
category: web
comments: true
---

The typical scenario is that you are using MAMP (or WAMP) to create a local installation of your Laravel application. This will work just fine until it's time to deploy your app to an production server.  
Then it's time for you to change the settings for the database connection. You could change them localy before you push the app to the production server, but then you would have to change back to the local settings later.  
You don't wanna do this. Instead, why don't you just set up a local environment in Laravel?  

####The steps

1. Open ``app/bootstrap/start.php``
2. Scroll down to the following section:  
    {% highlight php %}
    <?php
    $env = $app->detectEnvironment(array(
        'local' => array('your-machine-name'),
    ));
    {% endhighlight %}  
3. Replace 'your-machine-name' with 'localhost'.
4. Create a folder within ``app/config`` named 'local'.
5. Create a file named ``app/config/local/database.php`` (because this is the config file that we want to override.)
6. Write the following in database.php:
    {% highlight php %}
    <?php
    return array(
        'connections' => array(
            'mysql' => array(
                'driver'    => 'mysql',
                'host'      => 'localhost',
                'database'  => 'db',
                'username'  => 'root',
                'password'  => 'root',
                'charset'   => 'utf8',
                'collation' => 'utf8_unicode_ci',
                'prefix'    => '',
            ),
        )
    );
    {% endhighlight %}
This should look pretty familiar, right? It's exactly the same as the regular database.php, but only the part of it that you want to override.

