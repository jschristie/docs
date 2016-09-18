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

### Trust Relationship
