 
# IDP Initiated SSO with Gluu Server

An IdP Initiated SSO flow is a SSO operation that intiate from the IdP Security Domain. IdP server create a Federation SSO Response and redirecting the user to the SP with the response message. 
In this documentation we are going to see how we can configure a SSO which is IDP-initiated in Gluu Server. 

## Requirements

 - Required attributes from SP
 - Custom metadata which will be used in Gluu Server to configure Trust Relationship. 
   - We need to grab two values from SP side: 
      - EntityID of SP
      - Location to return users for authentication, ACS or Assertion Consumer Service
 - ProviderID value from SP. 

## Prepartion in Gluu Server

### Trust Relationsihp

 - Here is a sample metadata which we need to modify a bit for our desired SP. 
```
<EntityDescriptor entityID="entityID_of_SP"
    xmlns="urn:oasis:names:tc:SAML:2.0:metadata">
    <SPSSODescriptor AuthnRequestsSigned="false"
        WantAssertionsSigned="true" protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
        <NameIDFormat>urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified </NameIDFormat>
             <AssertionConsumerService isDefault="true"
                  index="0" Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-POST"
                  Location="ACS_location_of_SP" />
    </SPSSODescriptor>
</EntityDescriptor>
```
 - 
 - 
