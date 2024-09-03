# Ibexa Support Workshop 09/2024


- About DDEV
    - DDEV = ?
    - Installation
    - First Steps
- Ibexa DXP & DDV
    - doc.ibexa.co
    - Adding services
- Make Life easier - DDEV tools 
    - DDEV toolkit https://github.com/reithor/ibexa-ddev-toolkit
    - PR from Maciej Kobus - interactive DDEV setup (https://github.com/ibexa/website-skeleton/pull/14)
- DDEV and ... :
    - Personalization
    - Varnish
    - Fastly
    - Blackfire


Note:

---

##  About DDEV -  What is it?



<img class="scale40 center" style="background-color: black" src="/images/dark-ddev.svg" alt="DDEV" />

From https://ddev.com/

### "Docker-based PHP development environment"


_"Container superpowers with zero required Docker skills: environments in minutes, multiple concurrent projects, and less time to deployment."_


NOTE:

Keywords:
- zero Docker skills

--

##  About DDEV -  Installation



1. Step : Install Docker
2. Step : Install DDEV

- Easiest (and recommended) way on various OS : https://ddev.com/get-started/
- Detailed instructions (several options) :
https://ddev.readthedocs.io/en/stable/users/install/docker-installation/
https://ddev.readthedocs.io/en/stable/users/install/ddev-installation/



--

##  About DDEV -  First Steps


```
mkdir simple && cd simple

ddev config # confirm defaults for 'simple' example
ddev start 
echo '<?php phpinfo();' > index.php
ddev launch
ddev describe 
```
```
┌──────────────────────────────────────────────────────────────────────────────────────────────────────────────────┐
│ Project: simple /html/ddev/simple https://simple.ddev.site                                                       │
│ Docker platform: docker-desktop                                                                                  │
│ Router: traefik                                                                                                  │
├──────────┬──────┬───────────────────────────────────────────────────────────────────────────┬────────────────────┤
│ SERVICE  │ STAT │ URL/PORT                                                                  │ INFO               │
├──────────┼──────┼───────────────────────────────────────────────────────────────────────────┼────────────────────┤
│ web      │ OK   │ https://simple.ddev.site                                                  │ php PHP8.2         │
│          │      │ InDocker: web:443,80,8025                                                 │ nginx-fpm          │
│          │      │ Host: 127.0.0.1:63527,63528                                               │ docroot:''         │
│          │      │                                                                           │ Perf mode: none    │
│          │      │                                                                           │ NodeJS:20          │
├──────────┼──────┼───────────────────────────────────────────────────────────────────────────┼────────────────────┤
│ db       │ OK   │ InDocker: db:3306                                                         │ mariadb:10.11      │
│          │      │ Host: 127.0.0.1:63529                                                     │ User/Pass: 'db/db' │
│          │      │                                                                           │ or 'root/root'     │
├──────────┼──────┼───────────────────────────────────────────────────────────────────────────┼────────────────────┤
│ Mailpit  │      │ Mailpit: https://simple.ddev.site:8026                                    │                    │
│          │      │ Launch: ddev mailpit                                                      │                    │
├──────────┼──────┼───────────────────────────────────────────────────────────────────────────┼────────────────────┤
│ All URLs │      │ https://simple.ddev.site, https://127.0.0.1:63527,                        │                    │
│          │      │ http://simple.ddev.site, http://127.0.0.1:63528                           │                    │
└──────────┴──────┴───────────────────────────────────────────────────────────────────────────┴────────────────────┘
```

NOTE:
- show .ddev folder
- show traefik : http://localhost:10999/dashboard
- show ddev get --list / ddev get --list --all
---

### Ibexa DXP & DDV


## Install with DDEV
https://doc.ibexa.co/en/latest/getting_started/install_with_ddev/#installation


## DDEV and Ibexa Cloud
https://doc.ibexa.co/en/latest/ibexa_cloud/ddev_and_ibexa_cloud/



--

### Ibexa DXP & DDV - Adding services/add-ons

Adding services is in most cases done in 3 steps:

1. Require an addon using `ddev get`
2. Add configuration needed to make the addon work with Ibexa DXP
3. Reindex & restart the container 

Example:
```shell
  # get redis add-on
  ddev get ddev/ddev-redis
  
  echo "# " >> .env.local
  echo "# dxp-installer generated" >> .env.local
  echo "CACHE_POOL=cache.redis" >> .env.local
  echo "CACHE_DSN=redis:6379" >> .env.local
  
  echo "# dxp-installer generated" > .ddev/redis/redis.conf
  echo "maxmemory 9536870912" >> .ddev/redis/redis.conf
  echo "maxmemory-policy volatile-lfu" >> .ddev/redis/redis.conf
  
  ddev restart
  ddev php bin/console cache:clear
```

--
