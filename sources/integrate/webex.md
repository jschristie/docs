# How to configure Cisco WebEx with Gluu Server

## Configuration in Gluu Server

### Attributes

- 'WebexNameID'
  - Name: webexnameid
  - SAML1 URI: urn:gluu:dir:attribute-def:webexnameid
  - SAML2 URI: urn:oid:webexnameid
  - DisplayName: WebexNameID
  - Type: Text
  - Edit Type: admin
  - View Type: admin + user
  - Usage Type: Not definte
  - Multivalue: False
  - SCIM Attribute: False
  - Description: Custom nameID for WebEx, takes value from uid (through Shibboleth's config files)
  - ![WebexNameID attribute](https://raw.githubusercontent.com/docs/sources/img/SAMLTrustRelationships/webex_webexnameid.png)
- 'wxemail'
  - Name: email_webex
  - SAML1 URI: email
  - SAML2 URI: email
  - DisplayName: wxemail
  - Type: Text
  - Edit type: admin
  - View type: admin + user
  - Multivalue: False
  - SCIM Attribute: False
  - Description: Custom attribute for WebEX SSO. Pulling email from backend. 
  - 

### Trust Relationship
