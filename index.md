# Ibexa PX Workshop 09/2024


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
    - Varnish
    - Fastly
    - Personalization
    - Blackfire


Note:

---

##  About DDEV -  What is it?



<img class="scale40 center" style="background-color: black" src="/images/dark-ddev.svg" alt="DDEV" />

From https://ddev.com/

### "Docker-based PHP development environment"


_"Container superpowers with zero required Docker skills: environments in minutes, multiple concurrent projects, and less time to deployment."_



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

### Ibexa DXP & DDV - Docs

## Install with DDEV
https://doc.ibexa.co/en/latest/getting_started/install_with_ddev/#installation

## DDEV and Ibexa Cloud
https://doc.ibexa.co/en/latest/ibexa_cloud/ddev_and_ibexa_cloud/


--

### Ibexa DXP & DDV - Adding services/add-ons

Adding services is in most cases done in 4 main parts:

1. Require an "add-on" using `ddev get`
2. Add configuration needed to make the addon work with Ibexa DXP
3. Restart the container
4. Reindex and/or cache:clear 


Example:
```shell
  # get redis add-on
  ddev get ddev/ddev-redis
  
  echo "CACHE_POOL=cache.redis" >> .env.local
  echo "CACHE_DSN=redis:6379" >> .env.local
  
  echo "maxmemory 9536870912" >> .ddev/redis/redis.conf
  echo "maxmemory-policy volatile-lfu" >> .ddev/redis/redis.conf
  
  ddev restart
  ddev php bin/console cache:clear
```

---

### Make Life Easier - DDEV toolkit 

DDEV toolkit https://github.com/reithor/ibexa-ddev-toolkit


```shell

cd ~/
git clone git@github.com:reithor/ibexa-ddev-toolkit.git
ln -s ibexa-ddev-toolkit/ddev-dxp-installer.sh  ibexa_installer
# or create an alias - as you wish

#
```

```shell

# Call installer from anywhere
# Show "help" :
~/ibexa_installer

# Install Ibexa Experience in new subdirectory 'foo' :
# 'foo' will also be the ddev projectname and domain prefix  
~/ibexa_installer experience foo

# Add redis to current ddev project:
~/ibexa_installer add_redis

#
```

--

### Make Life Easier - interactive DDEV setup

Interactive DDEV setup: https://github.com/ibexa/website-skeleton/pull/14
(Hugely improved UX - by using https://github.com/charmbracelet/gum )


```

git clone -b ddev git@github.com:ibexa/website-skeleton.git ibexa-dxp
cd ibexa-dxp
ddev start

#
```

---

### DDEV and ... Varnish

```

# Add varnish to current ddev project:
~/ibexa_installer add_varnish 

```

``` tip

  [project-name].ddev.local will deliver content from varnish !
  
  novarnish.[project-name].ddev.local will show content as deliverd from the backend/app !
  
  Add X-User-Context-Hash to requests to 'mock' how varnish fetches content from the app
  Initial hash for anonymous user :
  daea248406c0043e62997b37292bf93a8c91434e8661484983408897acd93814
  
```

See also:

https://github.com/reithor/ddev-varnish

https://doc.ibexa.co/en/latest/infrastructure_and_maintenance/cache/http_cache/context_aware_cache/#context-aware-http-cache


--

### DDEV and ... Fastly

You need:
- A public URL that allows fastly to fetch content from your local app<br>
  ==> https://dashboard.ngrok.com/
- A Fastly service with *FASTLY_SERVICE_ID* and *FASTLY_KEY*<br>
  FASTLY_SERVICE_ID:
  ==> https://manage.fastly.com/configure/services/C5RrCFkVlRf9oTw5JR0I26
  FASTLY_KEY:
  ==> https://manage.fastly.com/account/tokens
- Run  `ddev composer require ibexa/fastly-forwarded-host`<br>
   --> ask Vidar why this is needed !
- A modified `ez_main.vcl` to skip ngrock warning<br>
  see: https://stackoverflow.com/questions/73017353/how-to-bypass-ngrok-browser-warning

--

### DDEV and ... Fastly

Change .env.local 
```
# .env.local
FASTLY_SERVICE_ID=C5RrCFkVlRf9oTw5JR0I26
FASTLY_KEY=gYkZ_qS1FX7sLoKkPo4Z4R8cikiXOi-6

HTTPCACHE_PURGE_SERVER=https://api.fastly.com
HTTPCACHE_PURGE_TYPE=fastly

#
```

Start ngrock:

```
ddev share --ngrok-args "--domain caribou-alert-roughly.ngrok-free.app"
```

Et voilà :

https://tre-dxp.global.ssl.fastly.net -> shows your app via fastly (actually 'my app')

--

### DDEV and ... personalization


Repo:
https://github.com/reithor/ibexa-ddev-toolkit/tree/personalization

Create Account:

https://doc.ibexa.co/projects/userguide/en/master/personalization/enable_personalization/#create-account


Set Credentials:

https://doc.ibexa.co/en/latest/personalization/enable_personalization/#get-authentication-parameters

Set up tracking:
https://doc.ibexa.co/en/latest/personalization/enable_personalization/#set-up-item-type-tracking


NOTE:
Ngrock:
https://dashboard.ngrok.com/
https://dashboard.ngrok.com/get-started/your-authtoken

https://doc.ibexa.co/en/latest/personalization/api_reference/tracking_api/




--

### DDEV and ... Blackfire


Login to github using support@ibexa.co:

https://github.com

Login to Blackfire using github auth:

https://blackfire.io/login

Check Auth params:

https://app.blackfire.io/envs/50d883ce-f002-441f-a690-0402cc8c7031/credentials



Setup DDEV for Blackfire:

https://docs.blackfire.io/integrations/paas/ddev


NOTE:

https://ibexa.atlassian.net/wiki/spaces/ENG/pages/5701714/Installation+via+Flex#Manual-installation-procedure-(for-development-branches)
