# Gluu Server SAML Proxy configuration


**Table of Contents**

- [Required items to configure Gluu SAML Proxy Server](#required-items)
- [Attribute Release Policy](#attribute-release)
- [Gluu Server Configuration](#gluu-server-configuration)
  - [Asimba Configuration](#asimba-configuration)
    - [Remote Authentication Server Configuration](#remote-authentication-server)
    - [SP Requestor configuration](#sp-requestors)
  - [Interception Script Configuration](#interception-script)
  - [Service Provide Trust Relationship](#sp-tr)
- [Gluu Asimba Extra Features](#extra-features)
- [Configure Gluu Server SAML Proxy ( Asimba server ) in Remote Authentication Server](#authn-server-tr)
- [Service Provider Configuration: Connect Gluu Server Shibboleth](#remote-sp-configuration)


The whole workflow will be:

```
Service Provider → Gluu Server with SAML Proxy → 
→ Gluu Server oxAuth interception Script ( SAML Script) → 
→ Gluu Server Proxy Server Discovery page  → Selected AuthN server → 
→ Gluu Server oxAuth(acr_values) → back_in reverser_order. 
```

## [Required items to configure Gluu SAML Proxy Server](#required-items)

  - Remote AuthN server metadata and SAML cert.
  - SP metadata. 
  - Required attributes for SAML AuthN and AuthZ

## [Attribute Release Policy](#attribute-release)

Required attributes of SP are configured in three sections: 
  - In Interception Script Configuration: 
    - saml_local_attributes_list
    - saml_idp_attributes_list
    - enforce_uniqueness_attr_list
  - Inside Trust Relationship of Gluu Server
  - From Remote AuthN Server ( IDP / ADFS ). 
  - 'transientID' is a default nameID in this whole scenario but other nameID can be configured as well. 

## [Gluu Server Configuration](#gluu-server-configuration)

To complete SAML Proxy configuration in Gluu Server we need to follow below: 

### [Asimba Configuration](#asimba-configuration)

#### [Remote Authentication Server Configuration](#remote-authentication-server)
  - Log into Gluu Server oxTrust
  - SAML --> IDPs
  - 'Add IDPs'
    - ID: The entityID of server
    - FriendlyName: Anything, whichever is suitable for you to differentiate specific server from long list
    - Metadata URL: Not required, we will use 'File' Method. But it's also possible to use internet accessible metadata location. 
    - Metadata Timeout: Timeout value if you use 'Metadata URL' to reach and read your remote metadata location. 
    - Metadata File: Upload xml format metadata by using 'Add' button if you haven't used 'Metadata URL' feature. 
    - Trust Certificate File: Upload x509 format SAML cert for your remote AuthN server; this certificate CAN NOT BE PASSWORD PROTECTED. 
    - NameIDFormat: Provide SAML2URI for your preferred nameID, you can keep it blank. 
    - Enabled: Yes
    - Send Scoping: Yes
    - AllowCreate: Yes
    - Disable SSO for IDP: By default 'NO'
    - ACS index: Yes
    - Send NameIDPolicy: Yes
    - Avoid Subject Confirmations: By default 'NO' 
    - Here is a sample setup: ![Image](https://raw.githubusercontent.com/GluuFederation/docs/master/sources/img/SAMLTrustRelationships/IDP_setup.png?raw=true)
  - For adding every IDP/AuthN server, administrator need to follow above steps.
  

#### [SP Requestor configuration](#sp-requestors)

  - Add 'oxAuth SAML' requestor. This requestor will act as SP in oxAuth interception script. 
  - Log into oxTrust
  - SAML --> SP Requestors
    - Add 'SP Requestor'
      - ID: `https://hostname_of_gluu_server/saml`
      - Friendly Name: oxAuth SAML
      - Metadata URL: leave it blank
      - Metadata Timeout: -1
      - Metadata File: Create a xml file with below snippet and upload new xml file.  
```
<!--Unsigned metadata for oxAuth-->
<md:EntityDescriptor xmlns:md="urn:oasis:names:tc:SAML:2.0:metadata" entityID="https://test.gluu.org/saml">
  <md:SPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:1.1:protocol urn:oasis:names:tc:SAML:2.0:protocol">
    <md:AssertionConsumerService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-POST" Location="https://test.gluu.org/oxauth/postlogin" index="0"/>
  </md:SPSSODescriptor>
  <md:Organization>
    <md:OrganizationName xml:lang="en">Gluu</md:OrganizationName>
    <md:OrganizationDisplayName xml:lang="en">Gluu - Open Source Access Management</md:OrganizationDisplayName>
    <md:OrganizationURL xml:lang="en">http://www.gluu.org</md:OrganizationURL>
  </md:Organization>
  <md:ContactPerson contactType="technical">
    <md:GivenName>Administrator</md:GivenName>
    <md:EmailAddress>support@gluu.org</md:EmailAddress>
  </md:ContactPerson>
</md:EntityDescriptor> </code>
      - Trust Certificate File: not required
      - Properties: leave it blank
      - 'Enabled': Yes
      - 'Signing': No
 
```
### [Interception Script Configuration](#interception-script)

We need to enable 'saml' interception script. 

  - Log into oxTrust
  - Configuration --> Manage Custom Script
  - For 'saml' script configuration: 
    - Name: saml
    - Description: saml authentication module
    - Programming Language: python
    - Level: 1
    - Location Type: LDAP
    - Usage Type: Web
    - Custom Properties ( Key/Value ): 
      - saml_deployment_type: enroll 
      - saml_name_identifier_format: urn:oasis:names:tc:SAML:2.0:nameid-format:persistent [ This is the name identifier or nameID for SSO transactions ] 
      - saml_idp_sso_target_url: https://hostname_of_gluu_server/asimba/profiles/saml2/sso/web [ Asimba discovery page which will allow end users to select their desired IDP for authentication ] 
      - saml_validate_response: false [ Specify if Saml script should valide Saml response signature. The path to IdP certificate should be specified in saml_certificate_file property. It's optional property. Default mode specify to validate Saml response. ] 
      - saml_use_authn_context: true [ Specify if Saml request should contains samlp:RequestedAuthnContext section. ] 
      - user_object_classes: eduPerson [ Define objectClasses which are required for enrollment other than 'top' and 'gluuPerson'. 'top' and 'gluuPerson' are default OCs shipped out of the box in Gluu Server ] 
      - saml_idp_attributes_list: urn:oid:0.9.2342.19200300.100.1.3, urn:oid:2.5.4.42, urn:oid:2.5.4.4, urn:oid:1.3.6.1.4.1.5923.1.1.1.6, urn:oid:0.9.2342.19200300.100.1.1 [ LDAP value of attributes which will be used in this SSO ] 
      - saml_local_attributes_list: mail, givenName, sn, edupersonprincipalname, uid [ Equivalent name of attributes which are enlisted in above idp_attributes_list ]
      - asimba_saml_certificate_file: /etc/certs/saml.pem [ SAML certificate of asimba server ] 
      - asimba_entity_id: https://hostname_of_gluu_server/saml [ EntityID of SAML Issuer ] 
      - enforce_uniqueness_attr_list: edupersonprincipalname 
    - Script: Grab script from [[https://github.com/GluuFederation/oxAuth/blob/master/Server/integrations/saml/SamlExternalAuthenticator.py|here]]
    - Sample interception script properties: ![Image](https://raw.githubusercontent.com/GluuFederation/docs/master/sources/img/interception_scripts/saml_script_properties.png?raw=true)

### [Service Provide Trust Relationship](#sp-tr)

Create Trust Relationship for every SP which will be connected in this SAML Proxy Single Sign On workflow. How to create Trust Relationship in Gluu Server is available [here](https://gluu.org/docs/integrate/outbound-saml/#how-to-create-trust-relationship).

## [Gluu Asimba Extra Features](#extra-features)

  - Discovery
If you want to allow your end users to select their own authentication server, the list of available IDPs can be shown in Discovery page. ![Image](https://raw.githubusercontent.com/GluuFederation/docs/master/sources/img/oxTrust/discovery_page.png?raw=true)
  - Selector
This feature 'automatically' forward users to specified Authentication server from service provider. As for example in below example user will automatically go to 'https://ce.gluu.info/idp/shibboleth' for authentication from 'https://ce.gluu.info/shibboleth' service provider. ![Image](https://raw.githubusercontent.com/GluuFederation/docs/master/sources/img/oxTrust/selector.png?raw=true)

## [Configure Gluu Server SAML Proxy ( Asimba server ) in Remote Authentication Server](#authn-server-tr)

We are using another Gluu Server as remote Authentication server. 

Create Trust Relationship here with Gluu SAML Proxy Server.
  - Log into oxTrust
  - SAML --> Trust Relationship
  - Add Relationship
    - Display Name: Nothing mandatory, anything you prefer
    - Description: Nothing mandatory, anything you prefer
    - Metadata Type: File
      - Upload Gluu SAML Proxy Server metadata. You will be able to get the SAML Proxy Server metadata with: `wget -c https://hostname_of_gluu_server/asimba/profiles/saml2`
    - Upload public certificate: Nothing required 
    - Configure specific RelyingParty: Yes. ![Image](https://raw.githubusercontent.com/GluuFederation/docs/master/sources/img/SAMLTrustRelationships/RelyingPartyConfigurationSAML2SSO.png?raw=true)
    - Released attribute: Whichever is preferable and required for SSO. Here in test setup we are releasing eduPersonPrincipalName, First Name, Last Name, TransientID and Username. ![Image](https://raw.githubusercontent.com/GluuFederation/docs/master/sources/img/SAMLTrustRelationships/testGluuOrgAsimba.png?raw=true)


## [Service Provider Configuration: Connect Gluu Server Shibboleth](#remote-sp-configuration)

This is just a standard Shibboleth SP configuration which will be configured as SP can talk to Gluu Server Shibboleth part. 
