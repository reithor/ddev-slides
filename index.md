##  About DDEV



<img class="scale40 center" style="background-color: black" src="/images/dark-ddev.svg" alt="DDEV" />

From https://ddev.com/

### "Docker-based PHP development environment"



---

### Ibexa DXP & DDV - Our Documentation

## Install with DDEV
https://doc.ibexa.co/en/latest/getting_started/install_with_ddev/#installation

## DDEV and Ibexa Cloud
https://doc.ibexa.co/en/latest/ibexa_cloud/ddev_and_ibexa_cloud/


---

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


```
# clone repo locally (or download from https://github.com/reithor/ddev-ibexa-installer/archive/refs/heads/main.zip )
git clone git@github.com:reithor/ddev-ibexa-installer.git ~/ddev-ibexa-installer


# new project 
mkdir installer_demo # create dir in directory where you usually store Webprojects
cd installer_demo
~/ddev-ibexa-installer/bin/create_project

# Existing local project checkouts can be initialized.
~/ddev-ibexa-installer/bin/init_project

#
```
