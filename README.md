<!--
N.B.: This README was automatically generated by https://github.com/YunoHost/apps/tree/master/tools/README-generator
It shall NOT be edited by hand.
-->

# Galène for YunoHost

[![Integration level](https://dash.yunohost.org/integration/galene.svg)](https://dash.yunohost.org/appci/app/galene) ![](https://ci-apps.yunohost.org/ci/badges/galene.status.svg) ![](https://ci-apps.yunohost.org/ci/badges/galene.maintain.svg)  
[![Install Galène with YunoHost](https://install-app.yunohost.org/install-with-yunohost.svg)](https://install-app.yunohost.org/?app=galene)

*[Lire ce readme en français.](./README_fr.md)*

> *This package allows you to install Galène quickly and simply on a YunoHost server.
If you don't have YunoHost, please consult [the guide](https://yunohost.org/#/install) to learn how to install it.*

## Overview

Galène is a videoconference server (an “SFU”) that is easy to deploy and that requires moderate server resources. It was originally designed for lectures and conferences (where a single speaker streams audio and video to hundreds or thousands of users), but later evolved to be useful for student practicals (where users are divided into many small groups), and meetings (where a dozen users interact with each other).

### Client features:

- multiparty audio and video
- text chat
- reasonably good support for mobile (Android and iPhone/iPad)
- screen and window sharing, including sharing multiple windows simultaneously (not on mobile)
- streaming video and audio from disk
- activity detection


**Shipped version:** 0.4.0~ynh2

**Demo:** https://galene.org:8443/

## Screenshots

![](./doc/screenshots/screenshot.png)

## Disclaimers / important information

### Accessing groups

*Galène* meeting rooms are called "groups". Any group is accessible at `https://domain.tld/group/GroupName`, by typing its name in the home page search field, or by selecting it in the public list (if the group is configured as publicly visible, see below).

#### Creating and configuring groups

Groups are defined by JSON files located in the folder `/home/yunohost.app/galene/groups`. Each group is represented by a `GroupName.json` file.
To create a new group, you need to create a `GroupNameExample.json` file (you can also make subfolder groups, and the groups will be accessible with `https://domain.tld/group/subfolder/GroupName`). Various configuration options are available (see https://github.com/YunoHost-Apps/galene_ynh/wiki/Configuration-file).

*NB: Spaces are supported in group file names.*

### Configuring your TURN server

#### Using *Galène*'s internal TURN server
Galène comes with a built-in TURN server that should work out-of-the-box.
- If your server is behind NAT, allow incoming traffic to TCP port `8443` (or whatever is configured with the `-http` option in `/etc/systemd/system/galene.service`) and TCP/UDP port `1194` (or whatever is configured with the `-turn` option in `/etc/systemd/system/galene.service`)

#### Using your own TURN server
- Install [coturn_ynh](https://github.com/YunoHost-Apps/coturn_ynh).
- Add `/opt/yunohost/galene/data/ice-servers.json` with these lines and change `turn.example.org` and `secret`

```
    [
        {
            "urls": [
                "turn:turn.example.org:5349",
                "turn:turn.example.org:5349?transport=tcp"
            ],
            "username": "galene",
            "credential": "secret"
        }
    ]
```
- set `/etc/systemd/system/galene.service` `-turn` option to `-turn auto` (or `-turn ""` to disable the built-in TURN server).

To check if the TURN server is up and running, type `/relay-test` in the chat box. If the TURN server is properly configured, you should see a message saying that the relay test has been successful.

You can also install Galène with an external TURN server with this branch: https://github.com/YunoHost-Apps/galene_ynh/tree/galene+turn 

### Server Statistics page

Statistics are available under `/opt/yunohost/galene/stats.json`, with a human-readable version at `domain.ltd/stats.html`. This is only available to the server administrator.

### How do I record my lecture?

Make sure allow-recording is set in your group configuration. Log-in as an operator, then say `/record` before you start your lecture. Don't forget to say `/unrecord` at the end. You will find your recordings under `https://server.example.com/recordings/groupname/`. The video recordings are stored in `/home/yunohost.app/galene/recordings` folder.


## Documentation and resources

* Official app website: https://galene.org/
* Official user documentation: https://galene.org/faq.html
* Official admin documentation: https://galene.org/
* Upstream app code repository: https://github.com/jech/galene
* YunoHost documentation for this app: https://yunohost.org/app_galene
* Report a bug: https://github.com/YunoHost-Apps/galene_ynh/issues

## Developer info

Please send your pull request to the [testing branch](https://github.com/YunoHost-Apps/galene_ynh/tree/testing).

To try the testing branch, please proceed like that.
```
sudo yunohost app install https://github.com/YunoHost-Apps/galene_ynh/tree/testing --debug
or
sudo yunohost app upgrade galene -u https://github.com/YunoHost-Apps/galene_ynh/tree/testing --debug
```

**More info regarding app packaging:** https://yunohost.org/packaging_apps