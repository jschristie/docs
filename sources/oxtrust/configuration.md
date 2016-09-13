[TOC]
# Configuration
This section of the documentation includes instructions for configuring
a number of the components of the Gluu Server in order to adjust the
server to your organizational needs.

![Configuration Menu](https://raw.githubusercontent.com/GluuFederation/docs/master/sources/img/oxTrust/config_menu.png)

# Organization Configuration
This section contains the following options:
- [System Configuration](#system-configuration)
- [Manage Email Addresses](#manage-email-addresses)
- [SMTP Server Configuration](#smtp-server-configuration)
- [oxTrust Configuration](#oxtrust-configuration)

## System Configuration
This feature allows the Gluu system administrator to customize and
implement various options such as *Cache Refresh*, *Federation Hosting*,
*SCIM Support* etc.

![System Configuration](https://raw.githubusercontent.com/GluuFederation/docs/2.4/sources/img/2.4/admin_config_system.png)

* _White Pages:_ If the user intends to use the built-in White Pages of
  the Gluu Server, this feature can be enabled here.

* _Self-Service Password Reset:_ The Self-Service Password Reset is
  disabled by default. For Self-Service Password Reset to work an SMTP
  server (see below) should be configured as well. Password reset link 
  for your Gluu server should be something like:
  "https://your.idp.link/identity/person/passwordReminder.htm".

* _SCIM Support:_ If the organization already has an identity management
  or provisioning system in place, the SCIM protocol can be used to push
  and synchronize the existing identity data into the Gluu Server.

* _DNS Server:_ The address of the DNS Server goes here.

* _Maximum Log Size:_ This option can be used to mitigate the space
  issues within the Gluu Server. The Gluu Server automatically zips any
  log file which is bigger than the defined value in this field.

* _User Can Edit Own Profiel:_ This option allows the user to edit his own profile which is located under `Personal`.

## SMTP Server Configuration
The Gluu server can communicate to any SMTP server specified in these
fields. All Gluu Server related informats *(cron daemon/logwatch/crash
reports etc.)* can be pushed to the desired Gluu Server administrator
using this feature.

![SMTP Server Configuration](https://raw.githubusercontent.com/GluuFederation/docs/2.4/sources/img/2.4/admin_config_smtp.png)

* _SMTP Host:_ Name of the SMTP host server.

* _From Name:_ Name of the Gluu Server administrator.

* _From Email Address:_ Email Address of the Gluu Server administrator.

* _Required Authentication:_ If the SMTP server requires authentication
  for every access, then enable this option by ticking the check-box,
  please.

* _SMTP User Name:_ The username for the SMTP server goes here.

* _SMTP Password:_ The password for the username above goes here. The
  username and password are used to access the SMTP server.

* _Requires SSL:_ If the SMTP Server offers communication via SSL enable
  this option by ticking the check-box.

* _SMTP Port:_ The number of the SMTP host server port has to be entered
  here.

## oxTrust Settings
This feature provides options to add various changes in the Gluu Server
User Interface. The Gluu Server administrator can add Title, Display
Name or even modify the Web User Interface color and logo from this
section.

![Configuration Panel](https://raw.githubusercontent.com/GluuFederation/docs/2.4/sources/img/2.4/admin_config_config.png)

* _Manager Group:_ The Gluu Server has a single manager group. The users
  that belong to the manager group can use the Web User Interface to
  operate the Gluu Server. There is no limit to the number of users that
  can be added to the manager group.

* _Organization Logo:_ The organization logo can be uploaded and
  activated from the configuration menu.

* _Organization Favicon:_ This feature can be used to change the
  organization favicon, if desired.

# Manage Authentication
This section allows the Gluu Server administrator to define how and
where the server should connect to authenticate users. If it is a remote
LDAP/Active Directory server, the values are required. Put the details
of the data source that you are trying to connect with Gluu Server. For
example, the data source can be your back-end Active Directory, or your
local LDAP server.

![Manage LDAP Authentication](https://raw.githubusercontent.com/GluuFederation/docs/2.4/sources/img/2.4/admin_manage_ldap.png)

* _Deactivate:_ This button *Deactivates/Activates* the Gluu Server
  accessibility for authentication.

* _Name:_ This field contains the name of the authentication server.

* _Bind DN:_ The *Username* for the authentication server (local
  LDAP/remote LDAP/remote Active Directory) goes here.

* _Use SSL:_ If the authentication server requires a secured port (i.e.
  636) then this option should be activated using the check-box.

* _Max Connections:_ This option can be used to define the total number
  of simultaneous connections allowed for reading local LDAP/remote Active
  Directory/remote LDAP.

* _Server:_ The unique name of the authentication server and port number
  (i.e. auth.company.org:636) goes here.

* _Base DN:_ Add base DNs in this field to allow the Gluu Server to
  connect and search the LDAP server. Every directory tree should be added
  separately using the *Add Base DN* option.

* _Primary Key:_ This field contains the primary key to connect to the
  authentication server (i.e. SAMAccountName/uid/mail etc.).

* _Local Primary Key:_ This field contains the internal LDAP primary key
  of the Gluu Server. Generally the key is either the *uid* or the *mail*.

* _Enabled:_ This check-box is used to enable the keys that are inserted
  in their respective fields.

* _Change Bind Password:_ This button assignes a password to
  authenticate the *Authentication Server*.

* _Test LDAP Connection:_ This button checks whether the provided
  information are sufficient to connect to the authentication server. The
  scan is done in real time, and it is recommended to be used by the Gluu
  Server administrators, only.

## Default Authentication Method

This allows the Gluu Server administrator to select both the default
authentication mode, and level for person authentication. Both modes are
set to "Default" until additional authentication mechanisms are enabled
via [custom scripts](#manage-custom-scripts).

Gluu Server uses oxAuth as the first step of authentication in all kind of SSO protocols ( OpenID Connect, SAML, CAS )

|Authentication Method|Description|
|---|---|
|Authentication mode|This mode is used in case of users authenticating with Gluu Server only without entring into oxTrust|
|oxTrust authentication mode|This mode is used for authenticate the GUI admins or users with oxTrust GUI access|

![Default Authentication Method](https://raw.githubusercontent.com/GluuFederation/docs/2.4/sources/img/2.4/admin_auth_default.png)

# Manage Custom Scripts  

The latest edition of the Gluu Server introduced a new Configuration
section called _Manage Custom Scripts_. This is a single place where the
server administrator can manage and implement interception scripts to
customize the behavior of the Gluu Server.

![Custom Authentication Scritp](https://raw.githubusercontent.com/GluuFederation/docs/master/sources/img/2.4/admin_auth_custom.png)

Please see the [Behaviour Customization page](../customize/script.md) for details.

# Manage Registration

![Image](https://raw.githubusercontent.com/GluuFederation/docs/master/sources/img/2.4/admin_config_workflow.png)

From the Manage Registration interface, the Gluu Server administrator
can customize the self-registration work-flow. Each option will be
covered individually as described below.

## Disable Captcha for registration form
Upon activating this feature, the default Captcha will be removed from
the registration form.

## Configure Registration Form Attributes
By default, there are a limited number of fields present in the
self-registration form. If more attributes are needed they can be added
in this section of Registration Management. Once you activate this
feature, just start typing the attribute name in the Attributes Filter
and then add desired attributes to the right column. Finally, click
"Update" to complete this step.

# Attributes
An *Active* attribute list can be seen from the Configuration >
Attributes section.

![Attribute Menu](https://raw.githubusercontent.com/GluuFederation/docs/master/sources/img/2.4/admin_attribute_menu.png)

The Gluu Server has a large LDAP tree which includes all standard
attributes. It is not necessary for all of them to be *Active*. The
active LDAP trees can be sorted using the *Show only Active Attributes*
link.

![Show Active Attribute](https://raw.githubusercontent.com/GluuFederation/docs/master/sources/img/2.4/admin_attribute_show.png)

The Gluu Server administrator can make changes, such as changing the
status to active/inactive, to an attribute after clicking on it.

![Attributes](https://raw.githubusercontent.com/GluuFederation/docs/master/sources/img/2.4/admin_attribute_attribute.png)

Additional attributes can be added from the Gluu Server GUI, oxTrust, by
clicking the **Add Attribute** button. Then, the following screen will
appear:

![Add Attribute Screen](https://raw.githubusercontent.com/GluuFederation/docs/master/sources/img/2.4/admin_attribute_add.png)

* _Name:_ This field defines the name of the custom attribute which must
  be unique in the Gluu Server LDAP tree.

* _SAML1 URI:_ This field contains the SAML1 uri for the custom attribute.

* _SAML2 URI:_ This field contains the SAML2 uri for the custom attribute.

* _Display Name:_ This display name can be anything that is human readable.

* _Type:_ The attribute type should be selected from the drop-down menu.
  There are four attribute types supported by Gluu:
  1. Text
  2. Numeric
  3. Photo
  4. Date

* _Edit Type:_ This field controls which type of an user is allowed to edit
  corresponding attribute at his/her "Profile" page of the web UI (when feature
"User can edit own profile" is enabled).

* _View Type:_ This field controls which type of an user is allowed to view
  corresponding attribute at his/her "Profile" page of the web UI.

* _Privacy Level:_ Please select the desired privacy level from the
  drop-down menu. The privacy level has a specific range of 1 to 5.

* _Multivalued:_ Please select multivalue in this field if the attribute
  contains more than one value.

* _SCIM Attributes:_ If the attribute is a part of SCIM architecture select true.

* _Description:_ This contains a few words to describe the attribute.

* _Status:_ The status, when selected active, will release and publish
  the attribute in IdP.

# Cache Refresh

**Cache Refresh** was built by Gluu to pull user information from a
backend customer Active Directory/LDAP Server. Cache refresh dynamically
synchronizes user information from the backend data source of the
customer to the Gluu Server in order to maximize performance. This
feature is sensitive in nature and any incorrect action may result in
loss of data within the Gluu Server. Before configuring Cache Refresh,
you should read the Cache Refresh overview (see Articles). For any
questions relating to Cache Refresh functionality, you can ask for
assistance from [Gluu Support](http://support.gluu.org). *For a
successful Cache Refresh setup, you have to insert data in ALL FIELDS
below.*

![Cache Refresh Menu](https://raw.githubusercontent.com/GluuFederation/docs/master/sources/img/2.4/admin_cache_menu.png)

* _Last Run:_ The date and time of the latest cache refresh cycle
  completion is shown here.

* _Updates at the Last Run:_ This shows the total number of users who
  have been updated in the last Cache Refresh cycle. For example an user
  who has any of his attribute updated will show up here.

* _Problem at the Last Run:_ This shows the number of users who have
  been rejected by the Gluu Server during the update. If there are any
  rejections, please contact Gluu Support for clarification and help.

![Last Run](https://raw.githubusercontent.com/GluuFederation/docs/master/sources/img/2.4/admin_cache_lastrun.png)

## Customer Backend Key and Attributes
![Customer Backend Key](https://raw.githubusercontent.com/GluuFederation/docs/master/sources/img/2.4/admin_cache_backend.png)

* _Key Attribute:_ This is the unique key attribute of backend Active
  Directory/LDAP Server such as SAMAccountname for any Active Directory.

* _Object Class:_ This contains the Object Classes of the backend Active
  Directory/LDAP which has permission to talk to Gluu Server Cache Refresh
  such as person, organizationalPerson, user etc.

* _Source Attribute:_ This contains the list of attributes which will be
  pulled and read by the Gluu Server.

* _Custom LDAP Filter:_ If there is any custom search required, this
filtering mechanism can be used such as "sn=*" whereas the value of this
field ensures that every user must contain an attribute named SN.

## Source Backend LDAP Servers
![Source Backend](https://raw.githubusercontent.com/GluuFederation/docs/master/sources/img/2.4/admin_cache_sourcebackend.png)

This section allows the Gluu Server to connect to the backend Active
Directory/LDAP server of the organization.

* _Name:_ Please input **source** as the value.

* _Use Anonymous Bind:_ Some customers do now allow username/password
  connections to their backend server. Enable this option if this applies
  to your organization.

* _Bind DN:_ This contains the username to connect to the backend
  server. You need to use full DN here. As for example,
  _cn=gluu,dc=company,dc=org_.

* _Use SSL:_ Use this feature if the backend server allows SSL
  connectivity.

* _Max Connections:_ This value defines the maximum number of
  connections that are allowed to read the backend Active Directory/LDAP
  server. It is recommended to keep the value of 2 or 3.

* _Server:_ This contains the backend Active Directory/LDAP server
  hostname with port i.e. backend.organization.com:389. If organization
  has a failover server, click **Add Server** and add more hostnames with
  port.

* _Base DN:_ This contains the location of the Active Directory/LDAP
  tree from where the Gluu Server shall read the user information.

* _Enabled:_ This check-box is used to save and push the changes. Do not
  use this unless the server administrator has entered all the required
  values.

* _Change Bind Password:_ This can be used for a new password or to
  change any existing password.

If your organization has a multiple Active Directory/LDAP server, click
on **Add source LDAP server** and add the additional server information.
Please remember that a *failover server* is not a new server.

## Inum LDAP Server

![Inum LDAP Server](https://raw.githubusercontent.com/GluuFederation/docs/master/sources/img/2.4/admin_cache_inum.png)

This section of the application allows the server administrator to
connect to the internal LDAP of the Gluu Server. As Gluu Server
administrator, you do not need to insert anything here in this section
as new Gluu Server versions automatically populates this for you (unless
you try to manually configure it anyway).

* _Refresh Method:_ The Gluu Server allows the Server Administrator to
  apply two types of Cache Refresh mechanism--(i) VDS Method and (ii) Copy
  Method.

  1. _VDS Method:_ Any organization with a database like *mysql* can use
  the VDS method. This option can be enabled via the drop-down menu in
  Refresh Method option.

![Refresh VDS](https://raw.githubusercontent.com/GluuFederation/docs/master/sources/img/2.4/admin_cache_refresh_vds.png)

  2. _Copy Method:_ If the organization has any kind of Active
  Directory/LDAP server, they are strongly recommended to use the *Copy
  Method* from the drop-down menu.

![Refresh Copy](https://raw.githubusercontent.com/GluuFederation/docs/master/sources/img/2.4/admin_cache_refresh_copy.png)

## Attributes Mapping

When the Copy method is selected, a section for Attribute mapping will
be exposed. In this section, the Gluu Server Administrator can map any
attribute from the backend Active Directory/LDAP to the LDAP cache of
the Gluu Server.

![Attribute Mapping](https://raw.githubusercontent.com/GluuFederation/docs/75518bb90184aa1b096874526b4da5f9f924bd44/sources/img/2.4/admin_cache_mapattribute.png)

In the source attribute to destination attribute mapping field, you can
enter the source attribute value on the left, and the destination
attribute on the right. In other words, you can specify what the
attribute is on the backend in the left field, and what it should be
rendered as when it comes through the Gluu Server in the right field.

The Administrator can select any Cache Refresh Method according to the
backend Active Directory/LDAP server, but there are some essential
values for both types of cache refresh method. The values are given
below.

  * _Pooling Interval (Minutes):_ This is the interval value for running
    the Cache Refresh mechanism in the Gluu Server. It is recommended to 
    be kept higher than 15 minutes.

  * _Script File Name:_ The Gluu Server cache refresh can accept any
    kind of Jython Script which might help to calculate any custom/complex
    attribute i.e. eduPersonScopedAffiliation. For more information please
    contact Gluu Support.

  * _Snapshot Folder:_ Every cycle of of Gluu Server Cache Refresh cycle
    saves an overall snapshot and problem-list record on a specified
    location. This is where the Gluu Server Administrator can specify the
    location. You can easily decide whether cache refresh synchronizes all
    users or not. Generally the rejected users are enclosed in the
    problem-list file. An overall report is displayed at the top of the
    cache refresh page with headings **Updated at the last run** and
    **Problems at the last run**.

  * _Snapshot Count:_ This defines the total number of snapshots that
    are allowed to be saved in the hard drive of the VM. It is recommended
    to be kept to 20 snapshots.

Latest Gluu Servers (including Community Edition) introduced two
upgraded sections here.

  * _Server IP Address:_ Include the IP of your Gluu Server here. This
    feature helps to run Cache Refresh mechanism perfectly in a clustered
    environment.

  * _Removed Script File Name location:_ New version of the Gluu Server
    allows the administrator to manage your custom scripts with more
    interactive section under configuration named Manage Custom Scripts.

  * _Update:_ This button is used to push the changes in the Gluu
    Server. Hit this button only when the values have been entered,
    completely.

  * _Update and Validate Script:_ This button is used to test the
    operation and integrity of any custom script such as a Jython Script.

# Configure Log Viewer

The Gluu Server has the facility to read log files using the GUI. The
log file can be displayed from the Web UI with a few clicks of the
mouse. This feature can be enabled from the configuration menu clicking
**Configuration --> Configure Log Viewer**.

![Configure Log Viewer](https://cloud.githubusercontent.com/assets/7703245/12272408/8fc7ecc2-b98a-11e5-9297-3d3f3329ba5d.png)

Gluu Server comes preloaded with four logs in this page as the screenshot portrays. The oxAuth, oxTrust, Cache Refresh and the console log is available by default.
Clicking on **Add log template** will bring up boxes where log path can be set to view the same from the GUI. The boxes on the
left contain the name/description of the log file, and the right boxes
contain the path of the log file such as _/opt/tomcat/logs/demo.log_.

# View Log File

The log files configured in the earlier section can be viewed using the
**View log file** feature. This feature can be accessed through the
configuration menu using **Configuration --> View Log File**.

![View Log File](https://raw.githubusercontent.com/GluuFederation/docs/master/sources/img/2.4/admin_view_log.png)

The **Display last lines count** field contains the lines that will be
displayed in the Web GUI. If the field contains the value **400**, then
the Gluu Server will show the last 400 lines of the log in the GUI. The
screenshot below shows an according example.

![Log file tail](https://raw.githubusercontent.com/GluuFederation/docs/master/sources/img/2.4/admin_view_logtail.png)

# Status

![Status](https://raw.githubusercontent.com/GluuFederation/docs/master/sources/img/2.4/admin_config_status.png)

The Status section provides a high level overview of server metrics. The
included values are straightforward and shouldn't require any further
explanation.
