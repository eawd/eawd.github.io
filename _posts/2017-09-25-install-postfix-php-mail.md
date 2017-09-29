---
layout: post
title:  "Setup PHP to use Postfix to send emails"
language: english
date: 2017-09-17 21:29:00 +0800
categories: php postfix
---

It might not be encouraged to install and use your own mailing server, but for testing purposes you may need to use it, so here is how I installed Postfix and set it up to send emails using PHP's mail function.

First you'll install postfix using the following command:

```bash
sudo apt-get install postfix
```

It will prompt you to enter a FQDN which is your top domain name e.g. `example.org`, It's well explained in the installation process so it shouldn't be a problem.
<!--description-->

To test your installation enter this command `sendmail -tif from@example.org to@example.com` Where *from@example.com* is the email you're sending from and *to@example.com* is the email you're sending to.
Write a message then press `Ctrl+d`, you should now find your message in *to@example.com* inbox or spam folders.

Now edit your proper php.ini file for me it was in `/etc/php/7.0/fpm/php.ini` and edit sendmail_path entry to be:

```
sendmail_path = "sendmail -tif from@example.org"
```

Again *from@example.com* will be the default email address used as the from email.

Now reload postfix and your server then you should be able to send emails using mail function from your server.

-----------
This serverfault answer helped a lot:

[https://serverfault.com/a/289290](https://serverfault.com/a/289290)

And as a bonus, here is how to configure Postfix to use sendgrid as a relay host.

[https://sendgrid.com/docs/Integrate/Mail_Servers/postfix.html](https://sendgrid.com/docs/Integrate/Mail_Servers/postfix.html)

----------