## How do I change the IP address and/or listening port of my Gluu Server?

There is no easy way to change the IP address or port of your Gluu Server once it's already deployed. At very least it would require to modify a lot of settings stored in LDAP configuration entries, in Apache/Tomcat configuration, and perhaps in custom authentication scripts' sources too (if you plan to use one). If you need to change an IP address, we recommend doing a fresh install on a new VM.

## How do I customize the IDP to ask for Email instead of Username for login? 

In oxTrust navigate to the Manage Authentication tab within the Configuration section. By default the Primary Key and Local Key are set to `uid`. Set those values to `mail` and now your Gluu Server will expect email as the identifier instead of username.

![Screenshot](https://raw.githubusercontent.com/GluuFederation/docs/master/sources/img/oxTrustConfiguration/Configuration/Authentication/Manage_Authentication_Primary_key_change.png)

Now you will want to update your IDP login page to display `Email Address` as the requested identifier. In order to do that you need to modify the `login.xhtml` file, which is located in `/opt/tomcat/webapps/oxauth/`. Insert `Email Address` as the value for `outputLabel`; this snippet is under the `dialog` class. See the screenshot below. 

![Screenshot](https://raw.githubusercontent.com/GluuFederation/docs/master/sources/img/oxTrustConfiguration/Configuration/Authentication/Email_Address.png)

## How do I add additional roles to oxTrust (Gluu's web UI) and/or change permissions set for existing ones

To accomplish something like that, you would need to implement new dynamic rules in Jboss Seam, and then implement those rules in the UI, as current "manager" and "user" roles are defined within `security.drl` and hard-coded in OxTrust. During login, it checks for the manager group's membership, and adds the role to the web context. If you'll still opt to change this framework, we won't be able to provide you any help regarding this currently.

oxTrust was designed to be a tool for administrators. There are some basic user features, but we don't really encourage usage of oxTrust as a user facing application.

A better approach might be to write a standalone application that calls the SCIM API's or even the LDAP API's with just the data that you want to expose. And make that new application an Openid Connect Relying Party (so authentication of users attempting to use it can be handled by the Gluu Server).

## How do I perform matinenace on my Gluu Server?

Sometimes it's required to push system updates (not an OS upgrade) in your Gluu Server VM. Here are a few steps to get you started:
   - Backup your whole VM.
   - Login to your Gluu Server VM.
   - Become root.
   - Login to the Gluu Server container using the following command: `service gluu-server-x.x.x login` (for RHEL/CentOS 7 users: `/sbin/gluu-server-x.x.x login`)
   - Push updates inside the container using the following command: `yum update` (for RPM based systems) or `apt-get update` (for DEB based systems).
   - Exit the container.
   - Stop Gluu-Server container using the following command: `service gluu-server-x.x.x stop` (for RHEL/CentOS 7users: `/sbin/gluu-server-x.x.x stop`).
   - Perform `yum update` or `apt-get update` in the host system.
   - Do a soft reboot.
   - After the VM returns from a succesful reboot, check the system status:
     - See if your Gluu Server container started by running the following command: `service gluu-server-x.x.x status`.
     - Login to the container. 
     - See if there is any issue in the `wrapper.log` file or in the `idp-process.log` file (if you are using SAML).
     - Wait for 10 minutes.
     - Check Gluu Server Web UI.
