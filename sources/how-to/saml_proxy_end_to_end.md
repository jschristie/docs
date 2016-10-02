# SAML Proxy End to End Configuration and Testing

## Preparation in Gluu Server
 
 During installation of Gluu Server, deployer need to select 'Asimba' for installation. After the completion of installation, we can move forward for rest of the work. 

### SAML custom script configuration

![SAML Script](https://github.com/GluuFederation/oxAuth/blob/master/Server/integrations/saml/SamlExternalAuthenticator.py) allows Gluu Server Administrator to prepare a complete SAML Proxy setup with their Gluu Server. 
To configure this custom script, 
 - Log into Gluu Server as admin user. 
 - Configuration -> Manage Custom Scripts
 - Select/Add 'saml' script from 'Person Authentication' tab
    - Name: saml
    - Description: Saml Authentication module
    - Programming Language: Python
    - Level: 1
    - Location Type: LDAP
    - Usage Type: Web
    - Custom property (key/value)
       - saml_deployment_type: enroll
       - saml_idp_sso_target_url: https://hostname_of_gluu_server/asimba/profiles/saml2/sso/web
       - saml_validate_response: false
       - asimba_entity_id: https://hostname_of_gluu_server/saml
       - asimba_saml_certificate_file: /etc/certs/saml.pem 
         - note: Deployer need to copy 'asimba.crt' in 'saml.pem' without any 'BEGIN CERTIFICATE' and 'END CERTIFICATE' tag. 
       - user_object_classes: eduPerson
       - saml_idp_attributes_mapping: { "attribute_name": ["attribute_name", "SAML2 URI"] } 
         - example: ```{"uid": ["uid", "urn:oid:0.9.2342.19200300.100.1.1"], "mail": ["mail", "urn:oid:0.9.2342.19200300.100.1.3"], "givenName": ["givenName", "urn:oid:2.5.4.42"], "sn": ["sn", "urn:oid:2.5.4.4"], "eduPersonPrincipalName": ["eduPersonPrincipalName", "urn:oid:1.3.6.1.4.1.5923.1.1.1.6"] } ```
       - enforce_uniqueness_attr_list: attribute1, attribute2
         - example: ```edupersonprincipalname, uid, mail, givenName```
       - saml_use_authn_context: false
       - saml_generate_name_id: true
       - enroll_all_attr: attribute3, attribute4 
         - example: ```memberOf, l```
    - Script: Grab script from github and paste it here. 
    - Enabled: True
    
### Asimba Configuration: 

#### Enroll Remote Authentication servers: 
    
  - Log into oxTrust as admin user
    - SAML -> IDPs
      - Add IDP
      - ID: The entityID of remote authentication server
        - example: ```https://nest.gluu.org/idp/shibboleth```
      - Friendly Name: Anything peferrable 
      - Metadata URL: Not required
      - Metadata Timeout: -1
      - Metadata File: Upload rermote IDP's xml metadata
      - Trust Certificate File: Uploade remote IDP's SAML certification. The format should be x509, crt; non password protected. 
      - NameIDFormat: Not required
      - Enabled: Yes
      - Send Scoping: Yes
      - AllowCreate: Yes
      - Disable SSO for IDP: No
      - ACS index: Yes
      - Send NameIDPolicy: Yes
      - Avoid Subject Confirmations: No
      
### SP Requestors: 

  - Log into oxTrust as admin user
  - 

 
## Preparation in Remote Authentication Server (IDP)

## Preparation in Service Provider (SP)
