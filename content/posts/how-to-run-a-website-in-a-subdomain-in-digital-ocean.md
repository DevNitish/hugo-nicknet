+++
author = "Nitish Kumar"
categories = ["Hack"]
date = 2021-09-14T02:48:00Z
description = ""
draft = false
image = "https://images.unsplash.com/photo-1502945015378-0e284ca1a5be?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&ixid=MnwxMTc3M3wwfDF8c2VhcmNofDMwfHxibG9nfGVufDB8fHx8MTYzMTY0NDQ2MQ&ixlib=rb-1.2.1&q=80&w=2000"
slug = "how-to-run-a-website-in-a-subdomain-in-digital-ocean"
tags = ["Hack"]
title = "How to run a website in a Subdomain in Digital Ocean"

+++

<!-- https://www.nicknetvideos.com/how-to-run-a-website-in-a-subdomain-in-digital-ocean/ -->
If you have a website and a single domain and a [Digital Ocean's](https://m.do.co/c/885fc9a6c5a4) droplet, and if you want to run the other website on a subdomain, then ****congratulations,**** you are at the right place.

I started my blog about 3 years ago using NodeJs, AngularJs, and a bunch of other technologies. I used Heroku free account to host it. But the bootup time for a free account in Heroku is so long that it used to annoy me, let alone the visitors on my site. So I shifted my blog on [Digital Ocean](https://m.do.co/c/885fc9a6c5a4), and the load time reduced drastically, and ****now my users are happy**** (That's what I hope they are).

But the problem came when I wanted to run my other projects on the same domain and on the same [Digital ocean](https://m.do.co/c/885fc9a6c5a4) account (means on the same Droplet. Who wants to pay more, to test things up.)

## Prerequisites

* [Digital Ocean Droplet](https://m.do.co/c/885fc9a6c5a4): If you don't have a Digital Ocean account, [register from here](https://m.do.co/c/885fc9a6c5a4) and get ****$100 in cloud credits****.
* You will also need a domain name. You can get it from Godaddy or Namecheap.
* We will use Nginx for our reverse proxy. Make sure you have [installed that on your Droplet](https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-ubuntu-16-04).
* Since this tutorial is for running your second Website on Nginx, make sure your first website is working fine. (Check out [this](https://www.digitalocean.com/community/tutorials/how-to-set-up-a-node-js-application-for-production-on-ubuntu-16-04) article for installing and running your Node app.)

We will use [`example.com`](http://example.com/) for the demo, make sure to update this with your website name.

First of all, we need to create a subdomain of our domain name. To do that, go to the DNS control panel of your domain name provider. There you have to create an ****"A record"**** for your subdomain.

We will name this _A record_ as `subdomain`so that we will have a subdomain as [`subdomain.example.com`](http://subdomain.example.com/). It should ****point**** to the IP address of your domain (eg. `145.87.XX.XX`). This way, you are setting as the destination for the host

Check out the tutorial to create an ****A record**** in [Godaddy](https://in.godaddy.com/help/create-a-subdomain-4080) or [Namecheap](https://www.namecheap.com/support/knowledgebase/article.aspx/9776/2237/how-to-create-a-subdomain-for-my-domain).

Log into your Droplet using [Putty](https://www.digitalocean.com/docs/droplets/how-to/connect-with-ssh/).

<div>
<style>
.tool__product {
    display: flex;
    align-items: center;
    justify-content: flex-start;
    min-height: 92px;
    padding: 16px 32px;
    margin: 40px 0;
    border-radius: 10px;
    background-color: #fff;
    box-shadow: 0 5px 10px rgb(154 160 185 / 5%), 0 15px 40px rgb(166 173 201 / 20%);
    cursor: pointer;
    transition: box-shadow .2s ease;
}
.tool__product-icon {
    flex: 0 0 auto;
    width: 33px;
    height: 35px;
    margin-right: 24px;
    background: url(https://www.nicknetvideos.com/content/images/2021/09/article.svg) no-repeat;
}

.tool__product-copy-container {
    display: flex;
    align-items: center;
    width: 100%;
}
.tool__product-copy {
    display: flex;
    flex-direction: column;
    width: 100%;
}
.tool__product-headline {
    color: #1c1e29;
    font-weight: 700;
}
.tool__product-note {
    color: #60657b;
}
.tool__product-button {
    display: flex;
    flex: 0 0 auto;
    align-items: center;
    justify-content: center;
    width: fit-content;
    height: 2.5rem;
    padding: 0 16px;
    margin-left: 24px;
    border-radius: 3px;
    background-color: #FF1A75;
    color: #fff;
    text-transform: uppercase;
}
@media screen and (max-width: 480px) {
  .tool__product, .tool__product>div {
    display: flex;
    padding-top: 1rem;
    flex-direction: column;
    align-items: center;
}
    .tool__product-headline{
    text-align: center;
    }
    .tool__product-copy, .tool__product-note{
        padding-bottom: 1rem;
    }
}


</style>

<a class="tool__product" data-portal="account/plans" href="#">
  <div class="tool__product-icon"></div>
  <div class="tool__product-copy-container">
    <div class="tool__product-copy">
      <div class="tool__product-headline">Tips to run your Blog</div>
      <div class="tool__product-note">Get the best viral stories straight into your inbox!</div>
    </div>
    <div class="tool__product-button">Sign-Up Today</div>
  </div>
</a>
</div>

If you have followed all the prerequisites, you must have a folder with the same name as your domain at a location `/var/www/example.com` here you will find all the files used to build your website.

We will create a new directory (or a folder) at `/var/www/` by typing `cd /var/www/` the `sudo mkdir` [`subdomain.example.com`](http://subdomain.example.com/) (provide password whenever asked by console) to create a new folder. After that, if you have a Node app, copy the files there and start the application or if you have a static website, copy the files into [`subdomain.example.com`](http://subdomain.example.com/) the folder.

> ****For Node App****: If you have a NodeJs app copy your files at `/var/www/subdomain.example.com` using [Filezilla](https://filezilla-project.org/). Use `npm start` or `pm2 start` (I recommend using [PM2 to run apps on droplet](https://www.digitalocean.com/community/tutorials/how-to-use-pm2-to-setup-a-node-js-production-environment-on-an-ubuntu-vps)) to start your node apps. Let's say your app starts running on port `3000`. Then type `sudo ufw allow 3000` because we need to set permission to allow port `3000` to be accessed by outsite world. To check that go to `[example.com](http://example.com/):3000` and check if it is running correctly.

## or

> ****For Static webpages****: If you want to server a static website copy your files at `/var/www/subdomain.example.com` using [Filezilla](https://filezilla-project.org/). Make sure you have an `index.html` at `/var/www/subdomain.example.com` folder. This is the page which will get rendered on hitting `[subdomain.example.com](http://subdomain.example.com/)`.

Now we will set a new server block in Nginx to call our new app. Goto, `/etc/nginx/sites-available/` here we will create a new file by typing `sudo vi` [`subdomain.example.com`](http://subdomain.example.com/) then press "i" to get into document edit mode. Type the following code:

****For Node App****:

```
server {
        listen 80;
        listen [::]:80;
        
        root /var/www/subdomain.example.com;
        index index.html index.htm index.nginx-debian.html;

        server_name subdomain.example.com;

        location / {

                proxy_pass http://localhost:3000;
                proxy_http_version 1.1;
                proxy_set_header Upgrade $http_upgrade;
                proxy_set_header Connection 'upgrade';
                proxy_set_header Host $host;
                proxy_cache_bypass $http_upgrade;
        }
}

```

## or

****For Static webpages****

```
server {
        listen 80;

        root /var/www/subdomain.example.com;
        index index.html index.htm index.nginx-debian.html;

        server_name subdomain.example.com www.subdomain.example.com;

        location / {
                try_files $uri $uri/ =404;
        }
}

```

Press `Esc` then `:wq` to save and exit the file.

Now you need to enable the configuration, make a symlink to the enabled sites:

```
ln -s /etc/nginx/sites-available/subdomain.example.com /etc/nginx/sites-enabled/subdomain.example.com

```

To check the syntax of code in the server block is correct:

```
sudo nginx -t

```

You will see a success message if the syntax used in the server file is correct.

To restart the Nginx server:

```
sudo systemctl restart nginx

```

If everything works fine, you will be able to see your new website at [`subdomain.example.com`](http://subdomain.example.com/).

If it works for you, comment "****Hell yes!****" otherwise mention any issue you faced.

<div class="col s12 mb-8">
<a href="https://www.digitalocean.com/?refcode=885fc9a6c5a4&utm_campaign=Referral_Invite&utm_medium=Referral_Program&utm_source=badge"><img src="https://web-platforms.sfo2.digitaloceanspaces.com/WWW/Badge%202.svg" alt="DigitalOcean Referral Badge" /></a>
</div>







