# Super Quick Ubuntu Shib Apache Install

Need to protect a test Apache folder using SAML on an Ubuntu server?
Hate to read? This article is for you. Replace both `minnow` and
`minnow.gluu.info` with your desired website hostname.

## Configure Apache

These are the steps to configure your Apache webserver properly:

```
# apt-get install apache2 libshibsp6 libapache2-mod-shib2
# a2enmod cgi
# a2enmod ssl
# a2enmod shib2
# a2ensite default-ssl
# mkdir /etc/certs
# cd /etc/certs
# openssl genrsa -des3 -out minnow.key 2048
# openssl rsa -in minnow.key -out minnow.key.insecure
# mv minnow.key.insecure minnow.key
# openssl req -new -key minnow.key -out minnow.csr
# openssl x509 -req -days 365 -in minnow.csr -signkey minnow.key -out minnow.crt
# shib-metagen -c /etc/certs/minnow.crt -h minnow.gluu.info > /etc/shibboleth/minnow-metadata.xml
# service apache2 start
# service shibd start
```

Download `minnow-metadata.xml` to your machine. You will need this file
later when you create the Trust Relationship in the Gluu Server.

```
# mkdir protected
# touch /var/www/protected/printHeaders.py
# chmod ugo+x /var/www/protected/printHeaders.py
```

Edit the default site at `/etc/apache2/sites-available/default-ssl.conf`, 
and add this part:

```
ScriptAlias /protected/ /var/www/protected/
<Directory /var/www/protected>
	AddHandler cgi-script .py
	Options +ExecCGI
	SSLOptions +StdEnvVars
	AuthType shibboleth
	ShibRequestSetting requireSession 1
	Require valid-user
</Directory>
```

Edit `printHeaders.py`, and add this simple script. It will show you the
HTTP headers:

```
#!/usr/bin/python

import os

d = os.environ
k = d.keys()
k.sort()

print "Content-type: text/html\n\n"

print "<HTML><HEAD><TITLE>Print Env Variables</TITLE></Head><BODY>"
print "<h1>Environment Variables</H1>"
for item in k:
	print "<p><B>%s</B>: %s </p>" % (item, d[item])
print "</BODY></HTML>"
```

# Configure the Shibboleth SP

Use this for `shibboleth2.xml` and replace `minnow.gluu.info` with the
hostname of your SP, and `brookie.gluu.info` with the hostname of your
IDP.

    <SPConfig xmlns="urn:mace:shibboleth:2.0:native:sp:config"
        xmlns:conf="urn:mace:shibboleth:2.0:native:sp:config"
        xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion"
        xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol"
        xmlns:md="urn:oasis:names:tc:SAML:2.0:metadata"
        logger="syslog.logger" clockSkew="180">
        <OutOfProcess logger="shibd.logger"> </OutOfProcess>
        <UnixListener address="shibd.sock"/>
        <StorageService type="Memory" id="mem" cleanupInterval="900"/>
        <SessionCache type="StorageService" StorageService="mem" cacheTimeout="3600" inprocTimeout="900" cleanupInterval="900"/>
        <ReplayCache StorageService="mem"/>
        <ArtifactMap artifactTTL="180"/>
        <RequestMapper type="Native">
            <RequestMap applicationId="default">
                <Host name="minnow.gluu.info">
                    <Path name="secure" authType="shibboleth" requireSession="true"/>
                </Host>
            </RequestMap>
        </RequestMapper>
        <ApplicationDefaults id="default" policyId="default"
            entityID="https://minnow.gluu.info/shibboleth"
            REMOTE_USER="eppn persistent-id targeted-id uid mail"
            signing="false" encryption="false" attributePrefix="SHIB_">
            <Sessions lifetime="28800" timeout="3600" checkAddress="false"
                handlerURL="https://minnow.gluu.info/Shibboleth.sso" handlerSSL="true"
                exportLocation="http://localhost/Shibboleth.sso/GetAssertion" exportACL="127.0.0.1"
                idpHistory="false" idpHistoryDays="7" cookieProps="; path=/; secure; httpOnly">
                <SessionInitiator type="Chaining" Location="/Login" isDefault="true" id="gluu"
                        relayState="cookie" entityID="https://brookie.gluu.info/idp/shibboleth">
                    <SessionInitiator type="SAML2" acsIndex="1" template="bindingTemplate.html"/>
                </SessionInitiator>
                <md:AssertionConsumerService Location="/SAML2/POST" index="1"
                    Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-POST"/>
                <md:AssertionConsumerService Location="/SAML2/POST-SimpleSign" index="2"
                    Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-POST-SimpleSign"/>
                <md:AssertionConsumerService Location="/SAML2/Artifact" index="3"
                    Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Artifact"/>
                <md:AssertionConsumerService Location="/SAML2/ECP" index="4"
                    Binding="urn:oasis:names:tc:SAML:2.0:bindings:PAOS"/>
                <md:AssertionConsumerService Location="/SAML/POST" index="5"
                    Binding="urn:oasis:names:tc:SAML:1.0:profiles:browser-post"/>
                <md:AssertionConsumerService Location="/SAML/Artifact" index="6"
                    Binding="urn:oasis:names:tc:SAML:1.0:profiles:artifact-01"/>
                <LogoutInitiator type="Chaining" Location="/Logout" relayState="cookie">
                    <LogoutInitiator type="SAML2" template="bindingTemplate.html"/>
                    <LogoutInitiator type="Local"/>
                </LogoutInitiator>
                <md:SingleLogoutService Location="/SLO/SOAP"
                    Binding="urn:oasis:names:tc:SAML:2.0:bindings:SOAP"/>
                <md:SingleLogoutService Location="/SLO/Redirect" conf:template="bindingTemplate.html"
                    Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect"/>
                <md:SingleLogoutService Location="/SLO/POST" conf:template="bindingTemplate.html"
                    Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-POST"/>
                <md:SingleLogoutService Location="/SLO/Artifact" conf:template="bindingTemplate.html"
                    Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Artifact"/>
                <md:ManageNameIDService Location="/NIM/SOAP"
                    Binding="urn:oasis:names:tc:SAML:2.0:bindings:SOAP"/>
                <md:ManageNameIDService Location="/NIM/Redirect" conf:template="bindingTemplate.html"
                    Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect"/>
                <md:ManageNameIDService Location="/NIM/POST" conf:template="bindingTemplate.html"
                    Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-POST"/>
                <md:ManageNameIDService Location="/NIM/Artifact" conf:template="bindingTemplate.html"
                    Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Artifact"/>
                <md:ArtifactResolutionService Location="/Artifact/SOAP" index="1"
                    Binding="urn:oasis:names:tc:SAML:2.0:bindings:SOAP"/>
                <Handler type="MetadataGenerator" Location="/Metadata" signing="false"/>
                <Handler type="Status" Location="/Status" acl="127.0.0.1"/>
                <Handler type="Session" Location="/Session" showAttributeValues="false"/>
            </Sessions>
            <Errors supportContact="you@example.com"
                logoLocation="/shibboleth-sp/logo.jpg"
                styleSheet="/shibboleth-sp/main.css"/>
            <RelyingParty Name="https://minnow.gluu.info" keyName="https://minnow.gluu.info"/>
            <MetadataProvider type="Chaining">
                    <MetadataProvider type="XML" url="https://brookie.gluu.info/idp/shibboleth" />
            </MetadataProvider>
            <TrustEngine type="Chaining">
                <TrustEngine type="ExplicitKey"/>
                <TrustEngine type="PKIX"/>
            </TrustEngine>
            <AttributeExtractor type="XML" validate="true" path="attribute-map.xml"/>
            <AttributeResolver type="Query" subjectMatch="true"/>
            <AttributeFilter type="XML" validate="true" path="attribute-policy.xml"/>
                    <CredentialResolver type="File" key="/etc/certs/minnow.key"
                            certificate="/etc/certs/minnow.crt" />
        </ApplicationDefaults>
    
        <SecurityPolicies>
            <Policy id="default" validate="false">
                <PolicyRule type="MessageFlow" checkReplay="true" expires="60"/>
                <PolicyRule type="Conditions">
                    <PolicyRule type="Audience"/>
                    <!-- Enable Delegation rule to permit delegated access. -->
                    <!-- <PolicyRule type="Delegation"/> -->
                </PolicyRule>
                <PolicyRule type="ClientCertAuth" errorFatal="true"/>
                <PolicyRule type="XMLSigning" errorFatal="true"/>
                <PolicyRule type="SimpleSigning" errorFatal="true"/>
            </Policy>
        </SecurityPolicies>
    </SPConfig>

Copy this file into `/etc/shibboleth/attribute-map.xml`:
```

<Attributes xmlns="urn:mace:shibboleth:2.0:attribute-map" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <Attribute name="urn:oid:2.5.4.42" id="givenName"/>
    <Attribute name="urn:oid:2.5.4.4" id="sn"/>
    <Attribute name="urn:oid:2.16.840.1.113730.3.1.241" id="displayName"/>
    <Attribute name="urn:oid:0.9.2342.19200300.100.1.1" id="uid"/>
</Attributes>
```

Now you need to create a Trust Relationship in your Gluu Server. Login,
go to SAML / Trust Relationships, and "Add Relationship":

![image](https://raw.githubusercontent.com/GluuFederation/docs/master/sources/img/ubuntu-shib-apache/minnow-saml-trust-relationship-shibboleth-sp.png)

Then, configure for SAML2SSO profile. Click on the checkbox to
"Configure specific RelyingParty":

![image](https://raw.githubusercontent.com/GluuFederation/docs/master/sources/img/ubuntu-shib-apache/configure_rp.png)

Then, click to add the SAML2SSO profile:

![image](https://raw.githubusercontent.com/GluuFederation/docs/master/sources/img/ubuntu-shib-apache/saml_sso-profile.png)

Then "Save" and "Update." Wait 5 minutes for the Shibboleth IDP to detect reload the metadata or
stop and start tomcat.

## Test

Test the CGI script at `https://minnow.gluu.info/protected/printHeaders.py`.
Enter both the valid username and password (like `admin` and your
initial admin password). The output will contain something like this:

    **Environment Variables**
    
    AUTH_TYPE: shibboleth
    CONTEXT_DOCUMENT_ROOT: /var/www/protected/
    CONTEXT_PREFIX: /protected/
    DOCUMENT_ROOT: /var/www/html
    GATEWAY_INTERFACE: CGI/1.1
    HTTPS: on
    HTTP_ACCEPT: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
    HTTP_ACCEPT_ENCODING: gzip, deflate, sdch
    HTTP_ACCEPT_LANGUAGE: en-US,en;q=0.8
    HTTP_CONNECTION: keep-alive
    HTTP_COOKIE: _shibsession_64656661756c7468747470733a2f2f6d696e6e6f772e676c75752e696e666f2f73686962626f6c657468=_6aab7e287072bcc123989d8bf5f0ed5e
    HTTP_DNT: 1
    HTTP_HOST: minnow.gluu.info
    HTTP_UPGRADE_INSECURE_REQUESTS: 1
    HTTP_USER_AGENT: Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/45.0.2454.85 Safari/537.36
    PATH: /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
    QUERY_STRING:
    REMOTE_ADDR: 192.168.88.1
    REMOTE_PORT: 52140
    REMOTE_USER: mike
    REQUEST_METHOD: GET
    REQUEST_SCHEME: https
    REQUEST_URI: /protected/printHeaders.py
    SCRIPT_FILENAME: /var/www/protected/printHeaders.py
    SCRIPT_NAME: /protected/printHeaders.py
    SERVER_ADDR: 192.168.88.133
    SERVER_ADMIN: webmaster@localhost
    SERVER_NAME: minnow.gluu.info
    SERVER_PORT: 443
    SERVER_PROTOCOL: HTTP/1.1
    SERVER_SIGNATURE:
    Apache/2.4.7 (Ubuntu) Server at minnow.gluu.info Port 443
    SERVER_SOFTWARE: Apache/2.4.7 (Ubuntu)
    SHIB_Shib_Application_ID: default
    SHIB_Shib_Authentication_Instant: 2015-09-17T01:13:23.278Z
    SHIB_Shib_Authentication_Method: urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport
    SHIB_Shib_AuthnContext_Class: urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport
    SHIB_Shib_Identity_Provider: https://brookie.gluu.info/idp/shibboleth
    SHIB_Shib_Session_ID: _6aab7e287072bcc123989d8bf5f0ed5e
    SHIB_Shib_Session_Index: _40e4b17668a13e0d406e41cc9f6bf116
    SHIB_displayName: Mike Schwartz
    SHIB_givenName: Michael
    SHIB_mail: mike@gmail.com
    SHIB_sn: Schwartz
    SHIB_uid: mike
    SSL_CIPHER: ECDHE-RSA-AES128-GCM-SHA256
    SSL_CIPHER_ALGKEYSIZE: 128
    SSL_CIPHER_EXPORT: false
    SSL_CIPHER_USEKEYSIZE: 128
    SSL_CLIENT_VERIFY: NONE
    SSL_COMPRESS_METHOD: NULL
    SSL_PROTOCOL: TLSv1.2
    SSL_SECURE_RENEG: true
    SSL_SERVER_A_KEY: rsaEncryption
    SSL_SERVER_A_SIG: sha256WithRSAEncryption
    SSL_SERVER_I_DN: emailAddress=mike@gluu.org,CN=minnow.gluu.info,O=Gluu,L=Austin,ST=TX,C=US
    SSL_SERVER_I_DN_C: US
    SSL_SERVER_I_DN_CN: minnow.gluu.info
    SSL_SERVER_I_DN_Email: mike@gmail.com
    SSL_SERVER_I_DN_L: Austin
    SSL_SERVER_I_DN_O: Gluu
    SSL_SERVER_I_DN_ST: TX
    SSL_SERVER_M_SERIAL: 9F5E4F891590BB53
    SSL_SERVER_M_VERSION: 1
    SSL_SERVER_S_DN: emailAddress=mike@gluu.org,CN=minnow.gluu.info,O=Gluu,L=Austin,ST=TX,C=US
    SSL_SERVER_S_DN_C: US
    SSL_SERVER_S_DN_CN: minnow.gluu.info
    SSL_SERVER_S_DN_Email: mike@gmail.com
    SSL_SERVER_S_DN_L: Austin
    SSL_SERVER_S_DN_O: Gluu
    SSL_SERVER_S_DN_ST: TX
    SSL_SERVER_V_END: Sep 10 18:46:32 2016 GMT
    SSL_SERVER_V_START: Sep 11 18:46:32 2015 GMT
    SSL_SESSION_RESUMED: Initial
    SSL_TLS_SNI: minnow.gluu.info
    SSL_VERSION_INTERFACE: mod_ssl/2.4.7
    SSL_VERSION_LIBRARY: OpenSSL/1.0.1f
    
## Troubleshooting 

 - Make sure you update your hosts file on the Gluu Server, Apache
   server, and your workstation--this won't work with IP addresses,
   only.

 - Check the Shibboleth log file `/opt/idp/logs/idp-process.log` if you
   don't see the headers or REMOTE_USER environment variables. Also,
   restart the Apache Tomcat service by `service tomcat restart` to 
   make sure the new Shibboleth IDP xml files were loaded.

 - Clear the cookies in your web browser for both the Apache site, and 
   the Gluu Server if you are logging in and logging out a lot with 
   lots of server restarts.

