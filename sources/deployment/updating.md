# Gluu Server Update Package
Gluu Server update packages are version specific released to enhance some features or to fix any unexpected bugs that might hinder the day-to-day performance 
of the Server. The first update package is released with Gluu Server Community Edition 2.4.4 and it is also available from the Gluu Repository easily installed with a yum/apt-get command.
## Requirements
The primary requirement for the update package is a working Gluu Server. It is highly recommended to `tar` the Gluu Server CE folder `/opt/gluu-server-2.4.4` 
to ensure speedy recovery from any unexpected hiccup. If your organization has any other contingtency plan, that is fine too.

!!! Warning
    Please make sure that there is enough disk space to tar the entire Gluu Server

* Use the following commands to tar the Gluu Server folder after logging into the Gluu `chroot`
`# tar cvf gluu-backup.tar /opt/gluu-server-2.4.4/`

## Install Update Package
Gluu Server update packages are available from the Gluu Repository.
Make sure to stop Gluu Server before installing and finalizing the update package.

* **CentOS 6.x/7.2, RHEL 6/7:** `yum install gluu-updater-2.4.4`

* **Ubuntu Server 14.04/16.04, Debian 8:** `apt-get install gluu-updater-2.4.4`

After the update package is installed, use the following commands to finalize the installation by running the update script. Remember to log into the Gluu Server `chroot` with the respective command.

!!! Note
    It is mandatory to log in to the Gluu Server chroot before running the following commands.

```
# cd /opt/upd/2.4.4.sp1/bin
# ./update_war.sh
```

It is recommended to wait a few minutes while the changes take place and Gluu Server CE can be used.

