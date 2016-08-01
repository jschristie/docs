[TOC]

# CentOS 7 Installation Guide
## Installing Gluu Server 
Download and install Gluu Server by the following commands. Use the
`.rpm` installation to perform a base chroot installation with the
following Gluu Server Base CentOS requirements.

As an alternative, use our Gluu repository for CentOS 7:

```
# wget https://repo.gluu.org/centos/Gluu-centos7.repo -O /etc/yum.repos.d/Gluu.repo
# wget https://repo.gluu.org/centos/RPM-GPG-KEY-GLUU -O /etc/pki/rpm-gpg/RPM-GPG-KEY-GLUU
# rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-GLUU
# yum clean all
# yum install gluu-server-2.4.3
```

## Configuring Gluu Server
After both the retrieval, and the installation of the Gluu Server
software package start the Gluu Server, and login into the local chroot
environment to configure the Gluu Server. These are the single steps:

```
# /sbin/gluu-serverd-2.4.3 start

# /sbin/gluu-serverd-2.4.3 enable

# /sbin/gluu-serverd-2.4.3 login

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

## Starting and Stopping the Gluu Server

You can start the Gluu Server with this command:

```
# /sbin/gluu-serverd-2.4.3 start
```

You can stop the Gluu Server with this command:

```
# /sbin/gluu-serverd-2.4.3 stop
```

## Login to the chroot environment

```
# /sbin/gluu-serverd-2.4.3 login
```

### Scripted Installation

If you want to script the installation of the Gluu Server, here is what
you can do to achieve your goal:

* Save and backup your existing file `setup.properties.last`.
* Uninstall existing Gluu Server installation.
* For a new installation you can either grab a new VM, or just use the
  existing one.
* Run all the commands until `# /sbin/gluu-serverd-2.4.3 login`.
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
# /sbin/gluu-serverd-2.4.3 stop

# yum remove gluu-server-2.4.3

# rm -rf /opt/gluu-server-2.4.3*
```

On an installation, any modified files are saved in the directory
`/opt/gluu-server24.save`. If you want to remove all the remnants of the
installation, delete these files with the command `rm -rf
/opt/gluu-server24.save'.

## Support

Gluu offers both community and VIP support. Anyone can browse and open
tickets on our [support portal](http://support.gluu.org). For private
support, expedited assistance, and strategic consultations, please view
[our pricing](http://gluu.org/pricing) and [schedule a meeting with
us](http://gluu.org/booking) to discuss VIP support options.
