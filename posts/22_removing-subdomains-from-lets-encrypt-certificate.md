---
title: Removing Subdomains From A Let’s Encrypt Certificate
template: templates/post.pug
date: 2018-03-22
author: Lenin Hasda
keywords: devops, ssl, letsencrypt, do, digitalocean, nginx, ubuntu
excerpt:

---

It's been a year since I started using SSL certificate from [Let's Encrypt](https://letsencrypt.org) and it's really easy to setup. I am using ubuntu on a [Digital Ocean](https://m.do.co/c/0042c103ddc7) droplet and followed their simple [tutorial to setup SSL for Nginx](https://www.digitalocean.com/community/tutorials/how-to-secure-nginx-with-let-s-encrypt-on-ubuntu-16-04#step-5-%E2%80%94-verifying-certbot-auto-renewal) using [Certbot](https://certbot.eff.org/).

I had a main domain and couple of subdomain and during setup when it prompt for domain selection I selected all of them. It did the job but with a twist, all the certification information were saved in single configuration file. Which was fine for a while until I deleted a subdomain.

Now after a year when I tried to update SSL I was getting error because of that deleted domain, it's certification information was still in that single configuration file. And according to [this thread](https://community.letsencrypt.org/t/how-to-delete-a-subdomain/22517/3) it's known limitation of Certbot that it's not possible to remove a domain from the certification file.

So here's how I solved the issue for my case:

**Step 1 - Always make a backup just in case**
```
sudo cp -r /etc/letsencrypt /etc/_letsencrypt
```

**Step 2 - Remove the old certificate information from these locations**
```
sudo rm -r /etc/letsencrypt/archive/<domain.tld>
sudo rm -r /etc/letsencrypt/live/<domain.tld>
sudo rm /etc/letsencrypt/renewal/<domain.tld.conf>
```
> Replace `domain.tld` with your configuration file name

**Step 3 - Remove all the certification references from Nginx conf**   
When you added the SSL Certbot adds the following lines in Nginx conf file which needs to be removed as well.

```
listen 443 ssl; # managed by Certbot
ssl_certificate /etc/letsencrypt/live/domain.tld/fullchain.pem; # managed by Certbot
ssl_certificate_key /etc/letsencrypt/live/domain.tld/privkey.pem;# managed by Certbot
include /etc/letsencrypt/options-ssl-nginx.conf; # managed by Certbot
ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem; # managed by Certbot

if ($scheme != "https") {
  return 301 https://$host$request_uri;
} # managed by Certbot
```

**Step 4 - Generate a new certificate**   
Finally I was ready to add new certificate but this time I didn't made the same mistake. This time I added certificate separately for each domain and subdomain.
```
sudo certbot --nginx -d example.com
sudo certbot --nginx -d sub1.example.com
sudo certbot --nginx -d sub2.example.com
# etc ...
```

**Step 5 - Reload Nginx**          
One last step was to reload the nginx server.
```     
sudo service nginx reload
```

This worked for me and I am pretty sure I can updated each domain and subdomain separately from now on.


#### Related reads:
- [Let's Encrypt](https://letsencrypt.org/)
- [Certbot](https://certbot.eff.org/)
- [Secure Nginx with Let's Encrypt on Digital Ocean](https://www.digitalocean.com/community/tutorials/how-to-secure-nginx-with-let-s-encrypt-on-ubuntu-16-04#step-5-%E2%80%94-verifying-certbot-auto-renewal)
- [Lets encrypt remove subdomains](https://airbladesoftware.com/notes/lets-encrypt-remove-subdomains/)

