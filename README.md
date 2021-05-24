

---

<!--
N.B.: This README was automatically generated by https://github.com/YunoHost/apps/tree/master/tools/README-generator
It shall NOT be edited by hand.
-->

# Galene for YunoHost

[![Integration level](https://dash.yunohost.org/integration/galene.svg)](https://dash.yunohost.org/appci/app/galene) ![](https://ci-apps.yunohost.org/ci/badges/galene.status.svg)  ![](https://ci-apps.yunohost.org/ci/badges/galene.maintain.svg)
[![Install galene with YunoHost](https://install-app.yunohost.org/install-with-yunohost.svg)](https://install-app.yunohost.org/?app=galene)

*[Lire ce readme en français.](./README_fr.md)*

> *This package allows you to install galene quickly and simply on a YunoHost server.
If you don't have YunoHost, please consult [the guide](https://yunohost.org/#/install) to learn how to install it.*

## Overview

Videoconferencing server that is easy to deploy

**Shipped version:** 0.3.5~ynh2

**Demo:** https://galene.org:8443/


## Screenshots


   ![](./doc/screenshots/screenshot.png)




## Disclaimers / important information

### How to creat groups

Groups are defined by files in the `/opt/yunohost/galene/groups` directory. Various options are available (see https://github.com/YunoHost-Apps/galene_ynh/wiki/Configuration-file)

### TURN server

For VoIP and video conferencing a TURN server is also installed and configured. The TURN server listens on two UDP and TCP ports. You can get them with these commands:

```
sudo yunohost app setting galene turnserver_port
```

The TURN server will also choose a port dynamically when a new call starts. The range is between 49152 - 65535.

For security reason the ports range (49152 - 65535) isn't automatically open by default. If you want to use Galène server for VoIP or conferencing you will need to open this port range manually. To do this, just run this command:

```
sudo yunohost firewall allow Both 49152:65535
```

You might also need to open these ports (if it is not automatically done) on your ISP box.

To prevent the situation when the server is behind a NAT, the public IP is written in the TURN server config. By this the TURN server can send its real public IP to the client. For more information see the [Coturn example config file](https://github.com/coturn/coturn/blob/master/examples/etc/turnserver.conf#L56-L62). So if your IP changes, you could run the script `/opt/yunohost/galene/Coturn_config_rotate.sh` to update your config.

If you have a dynamic IP address, you also might need to update this config automatically. To do that just edit a file named `/etc/cron.d/coturn_config_rotate` and add the following content.

```
*/15 * * * * root bash /opt/yunohost/galene/Coturn_config_rotate.sh;
```

To check if Galène can connect to the TURN server, connect to Galène as operator and type `/relay-test` in the chat box; if the TURN server is properly configured, you should see a message saying that the relay test has been successful.



## Documentation and resources

* Official app website: https://galene.org

* Official admin documentation: https://galene.org/
* Upstream app code repository:  https://github.com/jech/galene
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