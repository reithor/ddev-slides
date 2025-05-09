## DDEV Ibexa DXP Installer

Interactive installation tool for Ibexa DXP. Available options:

- DXP release
    - 4.6.x, 4.6.x dev, 5.0.x dev, 3.3,x
- PHP version
- Node version
- HTTP Servers
    - nginx-fpm, apache-fpm
- HTTP Cache
    - Varnish, Symfony's built in HTTP cache
- Database
    - MariaDB, MySQL, Postgres
- App cache
    - Redis, Memcached, Filesystem
- Search engine
    - Elasticsearch, Solr, Legacy

--

## Requirements

DDEV installed on your system:
<br>https://ddev.readthedocs.io/en/stable/users/install/ddev-installation/

For Ibexa Headless, Ibexa Experience, Ibexa Commerce a valid license is mandatory.
Adding a personal github OAUTH token is recommended. Composer auth config:


```shell

# .ddev/homeadditions/.composer/auth.json
{
    "github-oauth": {
        "github.com": "YOUR_OAUTH_TOKEN"
    },
    "http-basic": {
        "updates.ibexa.co": {
            "username": "INSTALLATION_KEY",
            "password": "INSTALLATION_TOKEN"
        },
    }
}

```

--

## Getting started

Clone ddev-ibexa-installer locally :
<br>(repo is private) 

```shell

git clone git@github.com:reithor/ddev-ibexa-installer.git ~/ddev-ibexa-installer


```

Create project:

```shell

mkdir installer_demo && cd installer_demo
~/ddev-ibexa-installer/bin/create_project


```

Kickstart from existing sources<br>(e.g. download from https://support.ibexa.co/Downloads/ibexa-dxp-v4.6-lts):

```shell

~/ddev-ibexa-installer/bin/init_project


```

---

##  DDEV


<img class="scale40 center" style="background-color: black" src="/images/dark-ddev.svg" alt="DDEV" />

From https://ddev.com/

### "Docker-based PHP development environment"



--

### Ibexa DXP & DDV - Ibexa Documentation

## Install with DDEV
https://doc.ibexa.co/en/latest/getting_started/install_with_ddev/#installation

## DDEV and Ibexa Cloud
https://doc.ibexa.co/en/latest/ibexa_cloud/ddev_and_ibexa_cloud/


--

### DDEV toolkit 

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

### Interactive DDEV setup - Maciej Kobus


Interactive DDEV setup: https://github.com/ibexa/website-skeleton/pull/14<br>
(Hugely improved UX - by using https://github.com/charmbracelet/gum )


```

git clone -b ddev git@github.com:ibexa/website-skeleton.git ibexa-dxp
cd ibexa-dxp
ddev start

#
```

--

### Interactive DDEV setup - Add-on

Interactive DDEV setup as DDEV Add-On : https://github.com/reithor/ddev-ibexa-installer/
<br>(Private repository)

```
# clone repo locally
# or download from https://github.com/reithor/ddev-ibexa-installer/archive/refs/heads/main.zip
git clone git@github.com:reithor/ddev-ibexa-installer.git ~/ddev-ibexa-installer


# new project 
mkdir installer_demo && cd installer_demo
~/ddev-ibexa-installer/bin/create_project

# Existing local project checkouts can be initialized.
~/ddev-ibexa-installer/bin/init_project

#
```
