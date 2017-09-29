---
title: How to use custom global functions in Yii2
template: templates/post.pug
date: 2016-08-24
author: Lenin Hasda
keywords: yii2, yii2 framework, custom function, function, global function, how to
---

I have been using yii2 for over a year now, and it was sad that I could find any simple way to use custom global functions. So far what I did was, make a **component** called **Utils** or **Tools** and put all my function there as static methods. Then when ever I needed them I used them like

```php
Utils::debug($variable)
```

and so on. It’s not like I hate to use it, but  I still wanted to have stand alone function. And I could not, it was sad and somewhat frustrating (some times).

Well, not anymore. I found a way to work around to be able to use custom global functions in my yii2 project. And this is how:

First create a directory to put your function file(s). In my case `common\helpers` , you can create it anywhere and name anything you want. I usually have two files, one called `utilities.php` to put all my small  utility functions, and another one called `functions.php` to put other larger functions. So my final directory looks like this:

```
|--backend
|--common
   |--helpers
      |--functions.php
      |--utilities.php
...
```

Then open up the composer.json file and add the following lines at the very end:

```
"autoload": {
    "files": [
        "common/helpers/functions.php",
        "common/helpers/utilities.php"
    ]
}
```

You can add as many files as you want in the same process.

Finally in the command line cd into your project directory and do the following command:

```
composer dump-autoload -o
```

If everything was right you should be able to see your files being included in `vendor/composer/autoload_files.php` file, and be able use the function(s) anywhere on your project.

Why this?? So that I can make and use dd (Laravel 😉 ) function to do debug and die. Even cooler I can have wordpress like `nav_menus` function to insert custom menu or `get_user_list` functions in my project.

I recently started using this, and so far only cons I found is that these files get included in every single request, whether i have used any function or not. If you find other issue feel free to comment below.

Till then, have fun!

