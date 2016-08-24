[TOC]

# Register User
Gluu Server offers a user registry service for the new users or if the organization lacks
any LDAP/AD. The registry service is already a part of the Gluu CE Installation but it is 
disabled by default. The custom-script feature of the Gluu Server is used to prepare the 
`User Registration`.

> Note: When possible, we recommend handling user registration in your app locally, then pushing the information to the Gluu Server via [SCIM 2.0](../api/scim-2.0.md). This will give you much more control and flexibility in defining the exact registration process you want users to go through.

## Preparing Gluu Server
The user registry requires enabling from the [custom scripts](../customize/script.md) section
of the Admin Panel. In brief, the admin has to click on the [configuration](../oxtrust/configuration.md) menu 
and navigate to `Manage Custom Scripts`.

![image](https://raw.githubusercontent.com/GluuFederation/docs/master/sources/img/2.4/config-manage-script_menu.png)

The tabs near the top of the page can be used to navigate to different custom scripts. We are concerned about 
the `User Registration` tab, it is placed third from the left.

![image](https://raw.githubusercontent.com/GluuFederation/docs/master/sources/img/2.4/config-manage-script_menu1.png)

The next step is to enable the user and set the value to `true` so that the user can login as soon as 
the registration is complete. So, set the `enable_user` property to `true`.

![image](https://raw.githubusercontent.com/GluuFederation/docs/master/sources/img/2.4/config-manage-script_enable.png)

The Script can be easily enabled by clicking on the checkbox at the bottom of the page.

![image](https://raw.githubusercontent.com/GluuFederation/docs/master/sources/img/2.4/config-manage-script_check.png)

## User Registration
The users can register through the user registration link usually available at `<hostname>/identity/register`.

![image](https://raw.githubusercontent.com/GluuFederation/docs/master/sources/img/2.4/config-manage-script_register.png)
