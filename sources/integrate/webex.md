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
  - Usage type: Not defined
  - Multivalue: False
  - SCIM Attribute: False
  - Description: Custom attribute for WebEX SSO. Pulling email from backend. 
  - ![wxemail](https://raw.githubusercontent.com/docs/sources/img/SAMLTrustRelationships/webex_wxemail.png)
- 'wxfirstname'
  - Name: firstname_webex
  - SAML1 URI: firstname
  - SAML2 URI: firstname
  - Display Name: wxfirstname
  - Type: Text
  - Edit Type: admin
  - View Type: admin + user
  - Usage Type: Not defined
  - Multivalued: False
  - SCIM Attribute: False
  - Description: Custom attribute for WebEX SSO, pulling 'givenname' from backend. 
  - ![wxfirstname](https://raw.githubusercontent.com/docs/sources/img/SAMLTrustRelationships/webex_wxfirstname.png)
- 'wxlastname'
  - Name: lastname_webex
  - SAML1 URI: lastname
  - SAML2 URI: lastname
  - Display Name: wxlastname
  - Type: Text
  - Edit Type: admin
  - View Type: admin + user
  - Usage Type: Not defined
  - Multivalued: False
  - SCIM Attribute: False
  - Description: Custom attribute for WebEX SSO, pulling 'sn' from backend. 
  - ![wxlastname](https://raw.githubusercontent.com/docs/sources/img/SAMLTrustRelationships/webex_wxlastname.png)
- 'wxuid'
  - Name: uid_webex
  - SAML1 URI: uid
  - SAML2 URI: uid
  - Display Name: wxuid
  - Type: Text
  - Edit Type: admin
  - View Type: admin + user
  - Usage Type: Not defined
  - Multivalue: False
  - SCIM Attribute: False
  - Description: Custom attribute for WebEX SSO, pulling 'uid' from backend. 
  - ![wxuid](https://raw.githubusercontent.com/docs/sources/img/SAMLTrustRelationships/webex_wxuid.png)

### Trust Relationship