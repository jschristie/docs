# Using SAML script without SAML Proxy ( Asimba ) in Gluu Server

This documentation is going to show us how to configure Gluu Server ( v 2.4.4 ) SAML Script without SAML Proxy server ( aka. Asimba ). 
For the preparation of this documentation we have used three servers: 
  - https://test.gluu.org ( Gluu Server whose SAML script we are going to use )
  - https://nest.gluu.org ( Remote Gluu Server which is going to act as AuthN server for end users )
  - https://sp.gluu.org ( Test service provider whose protected resources we are going to access through SSO )

## Configuration in test.gluu.org server

### SAML Custom Script setup: 
  - Log into oxTrust as admin user / user who has Gluu Server administrative priviledge
  - Configuration -> Manage Custom Scripts
  - Under 'Person Authentication' tab, scroll down to 'saml': 
    - Name: saml
    - Description: SAML Authentication module
    - Programming Language: Python
    - Level: 50
    - Location Type: Ldap
    - Usage type: Web
    - Custom property ( key/value ):
      - saml_certificate_file: /etc/certs/saml.pem ( Deployer need to grab the SAML cert of remote authentication server and place it here inside SAML_Script enabled Gluu Server as 'saml.pem'. Make sure that there is no "-----BEGIN CERTIFICATE-----" and "-----END CERTIFICATE-----" delimeter in saml.pem. As for example... in our case we saved ........................

## Configuration in nest.gluu.org server

## Configuration in sp.gluu.org
