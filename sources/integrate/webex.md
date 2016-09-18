# How to configure Cisco WebEx with Gluu Server

## Configuration in Gluu Server

### Attributes

- 'WebExEmail'
  - Name: email
  - SAML1 URI: urn:gluu:dir:attribute-def:email
  - SAML2 URI: urn:oid:0.9.2342.19200300.100.1.3
  - DisplayName: WebExEmail
  - Type: Text
  - Edit Type: admin
  - View Type: admin + user
  - Usage Type: Not definte
  - Multivalue: False
  - SCIM Attribute: False
  - Description: Custom email attribute for WebEx
  - ![WebExEmail attribute](https://raw.githubusercontent.com/GluuFederation/docs/sources/img/SAMLTrustRelationships/Attribute_creation_WebExEmail.png)

### Trust Relationship
