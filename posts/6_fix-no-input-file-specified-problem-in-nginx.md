---
title: Fix “No input file specified” problem in Nginx
template: templates/post.pug
date: 2016-06-26
author: Lenin Hasda
keywords: nginx, server, nginx config, 404 fix, no input fix
---

If you are using nginx server with php there is very good chance of getting **“No input file specified”** error, when you are expecting a **404 Not Found** page.

If you check the header of your request surprising you find a “404 Not Found” status but you get the “No input file specified” message, which is kind of weird.

What happens here is that even when Nginx receives a request for non-existent file with a .php extension, it passes the request to php-cgi. This happens because Nginx only checks if REQUEST_URL ends with a .php and not the actual file existence. But when php-cgi tries to process the request it fails because file doesn’t exist. So it sends “No input file specified” message with a “404 Not Found” header.

**Fix:**   

If you are running php-cgi on port 9000, you will have something like this (or similar) in your nginx config file:

```
location ~ .php$ {
    fastcgi_pass   127.0.0.1:9000;
    fastcgi_index  index.php;
    fastcgi_param  SCRIPT_FILENAME;
    ...
}
```

You just need to `try_files` to catch the 404 error and send proper error page:

```
location ~ .php$ {
    try_files $uri =404;
    fastcgi_pass   127.0.0.1:9000;
    fastcgi_index  index.php;
    fastcgi_param  SCRIPT_FILENAME;
    ...
}
```

Now you will get the proper 404 page for your non-existent files.

Note that this is not the only reason which could cause above issue. There are other reasons like wrong path sent to php-cgi and even permission issue as well. But this is most common reason for getting the above error message.

