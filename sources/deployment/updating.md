# Gluu Server Update Package

Gluu Server update packages are released to fix urgent issues, with low 
impact on deployment. Normally these involve updates to the java code,
effected replacing the `war` file. These are installed using 
`yum` or `apt-get` command.

## Requirements

It is highly recommended to stop the Gluu Server, and `tar` 
folder `/opt/gluu-server-2.4.4` to ensure speedy recovery from any 
unexpected hiccup. If your organization has other contingency plans,
that is ok too.

!!! Warning
    Please make sure that there is enough disk space to tar the entire 
    Gluu Server.

* Use the following commands to tar the Gluu Server folder from the host
OS:
`# tar cvf gluu-backup.tar /opt/gluu-server-2.4.4/`

## Install Update Package
Gluu Server update packages are available from the Gluu Repository.
Make sure to stop Gluu Server before installing and finalizing the 
update package.

* **CentOS 6.x/7.2, RHEL 6/7:** 

```
# yum install gluu-updater-2.4.4

```

* **Ubuntu Server 14.04/16.04, Debian 8:** 

```
# apt-get install gluu-updater-2.4.4

```

After the update package is installed, use the following commands to 
finalize the installation by running the update script. 

```
# service gluu-server-2.4.4 login
# cd /opt/upd/2.4.4.sp1/bin
# ./update_war.sh
```

It is recommended to wait a few minutes while the changes take place and 
Gluu Server CE can be used.
