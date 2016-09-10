[TOC]

# Debian 8 Installation Guide
## Installing Gluu Server 
Download and install Gluu Server by the following commands. Use the
`.deb` installation to perform a base chroot installation with the
following Gluu Server Base Ubuntu requirements.

As an alternative, use our Gluu repository for Debian Jessie (8):

```
# echo "deb https://repo.gluu.org/debian/ stable main" > /etc/apt/sources.list.d/gluu-repo.list

# curl https://repo.gluu.org/debian/gluu-apt.key | apt-key add -

# apt-get update

# apt-get install gluu-server-2.4.3
```

## Configuring Gluu Server
After both the retrieval, and the installation of the Gluu Server
software package start the Gluu Server, and login into the local chroot
environment to configure the Gluu Server. These are the single steps:

```
# /etc/init.d/gluu-server-2.4.3 start

# /etc/init.d/gluu-server-2.4.3 login

# cd /install/community-edition-setup/

#./setup.py
```

The `setup.py` script will bring up a prompt to provide information for certificate. It is recommened to use
`hostname.domain` structure for hostname and refrain from using `127.x.x.x`
for IP address. After the successful execution of `setup.py` script, login to oxTrust,
the policy administration point for Gluu. Point your browser to the uri
`https://hostname.domain`.

For both help and the latest
installation options see either [setup.py help](./setup_py.md), or run
`./setup.py -h`.

If you are not using a resolvable DNS host, you will need to add
the hostname to your hosts file on the server which is running your browser.
Login with the default user name “admin” and the password printed back in
the confirmation (also contained in `setup.properties.last` (use the
Unix command `grep --color -i pass` to find the according line quickly)
and look for the LDAP password which is the same as the admin password.

Make sure you remove or encrypt `setup.properties.last` It has the clear 
text passwords for everything: LDAP, admin user, keystores, and 3DES salt.
If something goes wrong, check `setup.log` for a detailed step-by-step
of the installation. As an alternative you may check the file
`setup_errors.log` to just see the errors (or stderr output from the
scripts).

## Removing/disabling Gluu repo

After initial installation is completed, it's recommended to remove Gluu
repos from sources list so you won't inadvertently upgrade your Gluu package by
conducting regular system's update procedures (like, by running `# yum update`)

Either remove `/etc/apt/sources.list.d/gluu-repo.list` file, or modify it
commenting out lines declaring Gluu CE's repos there.

## Starting and Stopping the Gluu Server

You can start the Gluu Server with this command:

```
# /etc/init.d/gluu-server-2.4.3 start

```

You can stop the Gluu Server with this command:

```
# /etc/init.d/gluu-server-2.4.3 stop

```

## Login to the chroot environment

```
# /etc/init.d/gluu-server-2.4.3 login

```

Or if you prefer...

```
# chroot /home/gluu-server24/ su -

```
### Scripted Installation

If you want to script the installation of the Gluu Server, here is what
you can do to achieve your goal:

* Save and backup your existing file `setup.properties.last`.
* Uninstall existing Gluu Server installation.
* For a new installation you can either grab a new VM, or just use the
  existing one.
* Run all the commands until `service gluu-server24 login`.
* Copy your file `setup.properties.last` into the new server's
  `/install/community-edition-setup/` location.
* Rename the file `setup.properties.last` to `setup.properties`.
* Run the setup script with `./setup.py` command.

## Uninstallation

First, exit from the chroot environment to main Linux.

Second, stop the Gluu Server chroot environment which will unmount all
chroot directories. As a third step, delete both the Gluu Server
packages that are installed, and the home directory of the Gluu Server
user. The following commands illustrate the single steps:

```
# service gluu-server-2.4.3 stop

# apt-get remove gluu-server-2.4.3

# rm -rf /opt/gluu-server-2.4.3*

```

On an installation, any modified files are saved in the directory
`/home/gluu-server24.save`. If you want to remove all the remnants of the
installation, delete these files with the command `rm -rf
/home/gluu-server24.save'.

In some circumstances, the installation can be broken. In that case
please try the following to force to uninstall the package.

```
# dpkg --purge --force-all gluu-server-2.4.3

```

## Support

Gluu offers both community and VIP support. Anyone can browse and open
tickets on our [support portal](http://support.gluu.org). For private
support, expedited assistance, and strategic consultations, please view
[our pricing](http://gluu.org/pricing) and [schedule a meeting with
us](http://gluu.org/booking) to discuss VIP support options.
