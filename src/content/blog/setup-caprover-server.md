---
title: "Caprover Server On VPS"
description: "Here is the basic setup a new Caprover server on a VPS for onclicked hosting"
pubDate: "Nov 17 2024"
heroImage: "/caprover-banner.png"
---

## What's Caprover ?

CapRover is an extremely easy to use app/database deployment & web server manager for your NodeJS, Python, PHP, ASP.NET, Ruby, MariaDB, MySQL, MongoDB, Postgres, WordPress (and etc...) applications!

It's blazingly fast and very robust as it uses Docker, nginx, LetsEncrypt and NetData under the hood behind its simple-to-use interface.

✔ CLI for automation and scripting\
✔ Web GUI for ease of access and convenience\
✔ No lock-in! Remove CapRover and your apps keep working!\
✔ Docker Swarm under the hood for containerization and clustering\
✔ Nginx (fully customizable template) under the hood for load-balancing\
✔ Let's Encrypt under the hood for free SSL (HTTPS)\

## Prequisites

**VPS**

- RAM: 4gb (Recommended)
- Ubuntu 20.04
- docker 19.03
- Public IP

**Domain name (Optional)**

- This is an option if you want your app be published or run as production
- Prepare a domain for caprover, e.g get domains as cheap as $1 on [NameCheap](https://www.namecheap.com/)

## Setup Caprover on VPS

#### Open/Allow on Firewall or Security Groups

```
ufw allow 80,443,3000,996,7946,4789,2377/tcp;
ufw allow 7946,4789,2377/udp;
```

#### Install Docker engine

**Set up Docker's apt repository**

```
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

**Install the Docker packages**

```
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

#### Caprover installation

**Install Carpover through Docker**

```
docker run -p 80:80 -p 443:443 -p 3000:3000 -v /var/run/docker.sock:/var/run/docker.sock -v /captain:/captain caprover/caprover
```

<div class="alert">
  <svg xmlns="http://www.w3.org/2000/svg" width="25" height="25" viewBox="0 0 24 16"><path fill="Orange" d="M13 14h-2V9h2m0 9h-2v-2h2M1 21h22L12 2z"/></svg>
  <strong>Warning: </strong>
  Do not change the specified ports, as caprover only works on specific ports
</div>

Once the CapRover is initialized, Visit `http://[IP_OF_YOUR_SERVER]:3000` in browser and login to CapRover using the default password `captain42`. After that, you can access Caprover Dashboard and deploy your app

<img alt="caprover-login" src="/caprover-login.png">

<img alt="caprover-dashboard" src="/caprover-dashboard.png">

**Custom domain for Caprover server**

Create an A record that maps a wildcard subdomain `*.[SUBDOMAIN]` to the IP address of your CapRover server

After that, go to Caprover Dashboard and connect your Domain with Caprover

<img alt="caprover-connect-subdomain" src="/caprover-connect-subdomain.png">

**Setup swap file for Linux**

In some cases, you may run into problems due to not having enough physical RAM. To work around these problems, you can set up a Swap file, by following these instructions on [How To Create A Linux Swap File](https://linuxize.com/post/create-a-linux-swap-file/?ref=franklinetech.com)
