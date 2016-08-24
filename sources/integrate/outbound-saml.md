**Table of Contents**  

- [Outbound SAML](#outbound-saml)
	- [Metadata of website:](#metadata-of-website)
	- [Required attribute of website:](#required-attribute-of-website)
	- [SSO testing endpoint of website:](#sso-testing-endpoint-of-website)
- [Configuring Outbound SAML SSO](#configuring-outbound-saml-sso)
	- [LDAP Attributes](#ldap-attributes)
	- [SAML Trust Relationship](#saml-trust-relationship)
		- [How to create Trust Relationship](#how-to-create-trust-relationship)

# Outbound SAML

Outbound SAML setup from Gluu Server is pretty easy using the Gluu
Server's oxTrust GUI. The following pieces of information are needed
from the target website or application:

- [Metadata of website](#metadata-of-website)
- [Required attribute of website](#required-attribute-of-website)
- [SSO testing endpoint of website](#sso-testing-endpoint-of-website)

The three points above are described briefly below.

## Metadata of website:

Metadata is a XML file which has configuration data used to provision any
website (SP) or IDP (Gluu Server) to communicate with each other. It is
interchangeable between the IDP and the SP.

Websites (SP) can provide metadata via URL or as a separate file. If the
SP provides an separate XML file, the Gluu Server can check the
integrity of that metadata with its own mechanism. This mechanism can be
shown and tested from Gluu Server oxTrust GUI.

## Required attribute of website:

Every organization has their own policy to release/share attributes with
any IDP or SP. The Gluu Server supports, and can be configured for
standard or custom attributes. This can be done from the Gluu Server
oxTrust GUI.

## SSO testing endpoint of website:

Every website (SP) should have both a staging and a production uri
endpoint which can be checked for SSO, where the user will access to log
into that SP.

# Configuring Outbound SAML SSO

The Gluu Server's SAML capabilities are tightly integrated with
[Shibboleth](https://shibboleth.net/).

## SAML Trust Relationship

A Trust Relationship is the mechanism to create single sign-on to any
SAML Service Provider (SP) from the Gluu Server SAML IDP. Trust
Relationships can be created from within the GUI.

### How to create Trust Relationship

In order to create a trust relationship with any SP:

* Go to SAML → Trust Relationships
* Click on “Add Relationship”
![Image](https://raw.githubusercontent.com/GluuFederation/docs/master/sources/img/SAMLTrustRelationships/Add_Relationships.png?raw=true)
* A new page will appear. Here, as a Gluu Server administrator you need
  to provide all the information regarding the SP to establish Trust
  Relationship from Gluu Server.
![Image](https://raw.githubusercontent.com/GluuFederation/docs/master/sources/img/SAMLTrustRelationships/TR_new_page.png?raw=true)
    * _Display Name_: Name of the Trust Relationship (it should be unique for every trust relationship)
    * _Description_: Little description. Purpose and SSO link can be added here.
    * _Metadata Type_: Depending on trusted party’s metadata (SP), there are four available types in Gluu Server
        * _File_: If SP has uploadable metadata in XML format, this option works best.
        * _URI_: If the metadata of SP has uri link and accessible from internet, Gluu Server Administrator need to use this option. 
        * _Generate_: Using Gluu Server to generate configuration files for SP is another big option when the SP is inhouse application or “Shibboleth SP” is installed or going to be installed in target application site (SP).  [How to install Shibboleth SP](http://www.gluu.org/docs/articles/apache-saml/) will help user to configure and install Shibboleth SP on their own area. Please note few things when you are going to use _Generate_ method for your SP. 
            * _URL_ : This is the `hostname of SP`
            * _Public certificate_ : You `must` have to provide the certificate which is Base64 encoded ASCII file and contain "-----BEGIN CERTIFICATE-----" and "-----END CERTIFICATE-----". This certificate `can not be password protected`. 
            * After creating the Trust Relationship, download the generated configuration files from `Download Shibboleth2 configuration files` link and place these configuration files inside your SP configuration. 

        * _Federation_: If target application ( SP ) is affiliated with any Federation server (i.e: InCommon, NJEdge etc. ), this option of “Metadata Type” is required. 
        Select “Federation” in Metadata Type and another drop down menu called “Select Federation” will appear. From this drop menu select desired Federation. 
        In order to create this documentation we took “InCommon” Federation as an example.
![Image](https://raw.githubusercontent.com/GluuFederation/docs/master/sources/img/SAMLTrustRelationships/Federation_1.png?raw=true)

After selecting the “Federation Name”, a new link named “Click to select
entity id” will appear. From this link Gluu Server Administrator can
select all SP’s entityIDs which are InCommon affiliated. Click on this
link and another new SP entityID discovery page will appear like below
image.

![Image](https://raw.githubusercontent.com/GluuFederation/docs/master/sources/img/SAMLTrustRelationships/Federation_2.png?raw=true)

Gluu Server Administrator can grab any SP’s entityID from “Filter” box.
As for example, Gluu Server Administrator is looking for Educause
entityID.

![Image](https://raw.githubusercontent.com/GluuFederation/docs/master/sources/img/SAMLTrustRelationships/Federation_3.png?raw=true)

* Public certificate: Upload the public certificate for this SP server.
  Please note that: public certificate’s CN (common name) MUST maintain
  the hostname of the SP server. If the SP has no certificate then keep
  this option blank and the IdP will generate a self signed certificate.

* Released: Release required attributes. Available attributes can be
  grabbed from upper left corner.

* More configuration: If the SP requires custom relying party and/or 
  custom MetadataFilter configuration, that can be achieved using the
  following options:
    * Configure MetadataFilters: Click on this option and Gluu Server
      will allow you to configure MetadataFilters inside the GUI.
    * Configure specific Relying Party: If the server admin “checks”
      this option a new link will appear which allows the server 
      administrator to modify various relying party configurations like
      SAML2SSO, SAML2AttributeQuery, ShibbolethSSO etc.

![image](https://raw.githubusercontent.com/GluuFederation/docs/master/sources/img/SAMLTrustRelationships/Relying_Party_Configuration.png)

After adding a new Trust Relationship, the server administrator will
observe a confirmation page like the one below. Please note that for
testing purposes we did not provide any certificates. The IdP created
both the key and certificate by itself. The image below shows a sample
Trust Relationship after successful creation.

Gluu Server administrator will be able to 'search' any trust relationship from 'Trust Relationship' search box. Searching syntax can be anything affiliated with specific Trust. It's also possible to see all Trusts by just hitting 'Search' button by keeping search box blank. ![image](https://raw.githubusercontent.com/GluuFederation/docs/master/sources/img/SAMLTrustRelationships/TR_all.png)
