[TOC]
# Schema

Below are the schemes for OpenDJ and OpenLDAP. The OpenDJ schema should
work for 389DS, too:

 * [OpenDJ](https://github.com/GluuFederation/community-edition-setup/tree/master/static/opendj)
 * [OpenLDAP](https://github.com/GluuFederation/community-edition-setup/tree/master/static/openldap)

## Object class gluuAppliance

 * __Description__ 
 * __blowfishPassword__ Blowfish crypted text
 * __c__ 
 * __description__ 
 * __displayName__ 
 * __gluuAdditionalBandwidth__ Track bandwidth requirements for the Gluu Server instance
 * __gluuAdditionalMemory__ Track additional memory requirements for the Gluu Server instance
 * __gluuApplianceDnsServer__ Persist the DNS server that should be used for the Gluu Server instance
 * __gluuAppliancePollingInterval__ Set the frequency of the health status update of the Gluu Server
 * __gluuBandwidthRX__ Track data received by the Gluu Server
 * __gluuBandwidthTX__ Track data sent by the Gluu Server
 * __gluuBillingEmail__ Billing alert email address
 * __gluuCentreonEmail__ TODO - in use? Email address to send monitoring alerts
 * __gluuDSstatus__ Monitor health of the instance LDAP server.
 * __gluuFederationHostingEnabled__ oxTrust flag for the federation feature. Values enabled or disabled
 * __gluuFreeDiskSpace__ Monitor free disk space on the Gluu Server instance
 * __gluuFreeMemory__ Monitor free memory on the Gluu Server instance
 * __gluuFreeSwap__ Monitor swap space on the Gluu Server instance
 * __gluuGroupCount__ Monitor the number of groups. TODO - Remove?
 * __gluuHTTPstatus__ Monitor HTTP availability of the Gluu Server instance
 * __gluuHostname__ The hostname of the Gluu Server instance
 * __gluuInvoiceNo__ TODO - in use?
 * __gluuIpAddress__ IP address of the Gluu Server instance
 * __gluuJiraEmail__ TODO - in use? Jira alert email address
 * __gluuLastUpdate__ Monitors last time the server was able to connect to the monitoring system
 * __gluuLifeRay__ None
 * __gluuLoadAvg__ Monitor the average CPU load for a Gluu Server instance
 * __gluuManageIdentityPermission__ TODO - in use?
 * __gluuManager__ Used to specify if a person has the manager role
 * __gluuMaxLogSize__ Maximum log file size
 * __gluuOrgProfileMgt__ enable or disable profile management feature in oxTrust
 * __gluuPaidUntil__ TODO - in use?
 * __gluuPaymentProcessorTimestamp__ TODO - in use?
 * __gluuPersonCount__ Monitor the number of people in the LDAP server for a Gluu Server instance
 * __gluuPrivacyEmail__ Privacy alert email address used by oxTrust
 * __gluuPrivate__ TODO - in use?
 * __gluuPublishIdpMetadata__ Gluu Server flag to publish the IDP metadata via the web server
 * __gluuResizeInitiated__ TODO - in use?
 * __gluuSPTR__ TODO - in use?
 * __gluuScimEnabled__ oxTrust SCIM feature - enabled or disabled
 * __gluuShibAssertionsIssued__ Monitors the activity of Gluu Server Shibboleth IDP
 * __gluuShibFailedAuth__ Monitors failed login attempts on Gluu Server Shibboleth IDP
 * __gluuShibSecurityEvents__ Monitors security events on Gluu Server Shibboleth IDP
 * __gluuShibSuccessfulAuths__ Monitors login attempts on Gluu Server Shibboleth IDP
 * __gluuSmtpFromEmailAddress__ SMTP From email address
 * __gluuSmtpFromName__ SMTP From name
 * __gluuSmtpHost__ SMTP host
 * __gluuSmtpPassword__ SMTP user password
 * __gluuSmtpPort__ SMTP port
 * __gluuSmtpRequiresAuthentication__ SMTP requires authentication
 * __gluuSmtpRequiresSsl__ SMTP requires SSL
 * __gluuSmtpUserName__ SMTP user name
 * __gluuSslExpiry__ SAML trust relationship configuration
 * __gluuStatus__ Status of the entry, used by many object classes
 * __gluuSvnEmail__ SVN alert email address
 * __gluuSystemUptime__ Monitors how long the Gluu Server instance has been running
 * __gluuTargetRAM__ Monitors total available RAM on the Gluu Server instance
 * __gluuUrl__ Gluu Server instance uri
 * __gluuVDSenabled__ oxTrust VDS enabled or disabled
 * __gluuVDSstatus__ Gluu VDS configuration
 * __gluuVdsCacheRefreshEnabled__ None
 * __gluuVdsCacheRefreshLastUpdate__ None
 * __gluuVdsCacheRefreshLastUpdateCount__ None
 * __gluuVdsCacheRefreshPollingInterval__ None
 * __gluuVdsCacheRefreshProblemCount__ None
 * __gluuWhitePagesEnabled__ None
 * __iname__ None
 * __inum__ XRI i-number (iNum)
 * __inumFN__ XRI i-number (iNum) without punctuation
 * __o__ 
 * __oxAuthenticationLevel__ None
 * __oxAuthenticationMode__ None
 * __oxClusterType__ Type of the underlying clustering mechanism
 * __oxClusteredServers__ List of the clustering partners of this server
 * __oxIDPAuthentication__ Custom IDP authentication configuration
 * __oxLogViewerConfig__ Log viewer configuration
 * __oxMemcachedServerAddress__ Initialization string for memcached client
 * __oxSmtpConfiguration__ SMTP configuration
 * __oxTrustStoreCert__ oxPush device configuration
 * __oxTrustStoreConf__ oxPush application configuration
 * __passwordResetAllowed__ Is password reset mechanics allowed
 * __softwareVersion__ None
 * __userPassword__ 
 * __oxTrustCacheRefreshServerIpAddress__ None

## Object class gluuAttribute

 * __Description__ 
 * __description__ 
 * __displayName__ 
 * __gluuAttributeEditType__ Specify in oxTrust who can update an attribute - admin or user
 * __gluuAttributeName__ Specify an identifier for an attribute. May be multi-value where an attribute has two names, like givenName and first-name
 * __gluuAttributeOrigin__ Specify the person object class associated with the attribute, used for display purposes in oxTrust
 * __gluuAttributeSystemEditType__ TODO - still required?
 * __gluuAttributeType__ Data type of attribute. Values can be string, photo, numeric, and date
 * __gluuAttributeUsageType__ TODO - Usage? Value can be OpenID
 * __gluuAttributeViewType__ Specify in oxTrust who can view an attribute -  admin or user
 * __gluuCategory__ TODO - in use? Used to group attributes together
 * __gluuSAML1URI__ SAML 1 uri of attribute
 * __gluuSAML2URI__ SAML 2 uri of attribute
 * __gluuStatus__ Status of the entry, used by many object classes
 * __iname__ None
 * __inum__ XRI i-number
 * __objectClass__ 
 * __oxAttributeType__ NameId or attribute
 * __oxMultivaluedAttribute__ None
 * __oxNameIdType__ NameId type
 * __oxSCIMCustomAttribute__ None
 * __oxSourceAttribute__ Source attribute for this attribute
 * __seeAlso__ 
 * __urn__ None
 * __oxAuthClaimName__ Used by oxAuth in conjunction with gluuLdapAttributeName to map claims to attributes in LDAP.

## Object class gluuGroup

 * __Description__ 
 * __c__ 
 * __description__ 
 * __displayName__ 
 * __gluuGroupType__ Type of group. Not used
 * __gluuGroupVisibility__ Group visibility. Not used
 * __gluuStatus__ Status of the entry, used by many object classes
 * __iname__ None
 * __inum__ XRI i-number (iNum)
 * __member__ 
 * __o__ 
 * __owner__ 
 * __seeAlso__ 

## Object class gluuInumMap

 * __Description__ 
 * __gluuStatus__ Status of the entry, used by many object classes
 * __inum__ XRI i-number (iNum)
 * __primaryKeyAttrName__ Primary key attribute name
 * __primaryKeyValue__ Primary key value
 * __secondaryKeyAttrName__ Secondary key attribute name
 * __secondaryKeyValue__ Secondary key value
 * __tertiaryKeyAttrName__ Tertiary key attribute name
 * __tertiaryKeyValue__ Tertiary key value

## Object class gluuInvoice

 * __Description__ 
 * __gluuInvoiceAmount__ TODO - in use?
 * __gluuInvoiceDate__ TODO - in use?
 * __gluuInvoiceLineItemName__ TODO - in use?
 * __gluuInvoiceNumber__ TODO - in use?
 * __gluuInvoiceProductNumber__ TODO - in use?
 * __gluuInvoiceQuantity__ TODO - in use?
 * __gluuInvoiceStatus__ TODO - in use?
 * __inum__ XRI i-number

## Object class gluuOrganization

 * __Description__ 
 * __c__ 
 * __county__ ISO 3166-1 Alpha-2 country code
 * __deployedAppliances__ Track which appliances are deployed at an organization
 * __description__ 
 * __displayName__ 
 * __gluuAddPersonCapability__ Organizational attribute to control whether new users can be added via the oxTrust GUI
 * __gluuAdditionalUsers__ TODO: use unclear
 * __gluuApplianceUpdateRequestList__ Used by the Gluu Server to request an update
 * __gluuCustomMessage__ oxTrust custom welcome message
 * __gluuFaviconImage__ TODO - Stores uri of Gluu Server favicon
 * __gluuFederationHostingEnabled__ oxTrust flag for the federation feature. Values enabled or disabled
 * __gluuInvoiceNo__ TODO - in use?
 * __gluuLogoImage__ Logo used by oxTrust for default look and feel
 * __gluuManageIdentityPermission__ TODO - in use?
 * __gluuManager__ Used to specify if a person has the manager role
 * __gluuManagerGroup__ Used in organization entry to specifies the DN of the group that has admin privileges in oxTrust
 * __gluuOrgProfileMgt__ enable or disable profile management feature in oxTrust
 * __gluuOrgShortName__ Short description, as few letters as possible, no spaces
 * __gluuOwnerGroup__ Deprecated. Use gluuManagerGroup, instead.
 * __gluuPaidUntil__ TODO - in use?
 * __gluuPaymentProcessorTimestamp__ TODO - in use?
 * __gluuProStoresUser__ TODO - remove
 * __gluuStatus__ Status of the entry, used by many object classes
 * __gluuTempFaviconImage__ Store location for upload of the Gluu Server favicon
 * __gluuThemeColor__ oxTrust login page configuration
 * __gluuWhitePagesEnabled__ None
 * __iname__ None
 * __inum__ XRI i-number (iNum)
 * __l__ 
 * __mail__ 
 * __memberOf__ None
 * __nonProfit__ TODO - in use?
 * __o__ 
 * __objectClass__ 
 * __oxCreationTimestamp__ Registration time
 * __oxLinkLinktrack__ Linktrack link
 * __oxLinktrackEnabled__ Is Linktrack API configured
 * __oxLinktrackLogin__ Linktrack API login
 * __oxLinktrackPassword__ Linktrack API password
 * __oxRegistrationConfiguration__ Registration configuration
 * __postalCode__ 
 * __proStoresToken__ None
 * __prostoresTimestamp__ None
 * __scimAuthMode__ SCIM authorization mode
 * __scimGroup__ SCIM group
 * __scimStatus__ SCIM status
 * __st__ 
 * __street__ 
 * __telephoneNumber__ 
 * __title__ 
 * __uid__ 
 * __userPassword__ 

## Object class gluuPasswordResetRequest

 * __Description__ 
 * __creationDate__ Creation date used for password reset requests
 * __oxGuid__ A random string to mark temporary tokens
 * __personInum__ iNum of a person

## Object class gluuPerson

 * __Description__ 
 * __associatedClient__ 
 * __c__ 
 * __displayName__ 
 * __givenName__ 
 * __gluuManagedOrganizations__ Used to track the organizations a person is associated with
 * __gluuOptOuts__ White pages attributes restricted by person in oxTrust profile management
 * __gluuStatus__ Status of the entry, used by many object classes
 * __gluuWhitePagesListed__ Allow publication
 * __iname__ None
 * __inum__ XRI i-number (iNum)
 * __mail__ 
 * __memberOf__ None
 * __o__ 
 * __oxAuthPersistentJWT__ oxAuth persistent JWT
 * __oxCreationTimestamp__ Registration time
 * __oxExternalUid__ None
 * __oxInviteCode__ Invite Code
 * __oxLastLogonTime__ Last logon time
 * __oxTrustActive__ None
 * __oxTrustAddresses__ None
 * __oxTrustEmail__ None
 * __oxTrustEntitlements__ None
 * __oxTrustExternalId__ None
 * __oxTrustImsValue__ None
 * __oxTrustMetaCreated__ None
 * __oxTrustMetaLastModified__ None
 * __oxTrustMetaLocation__ None
 * __oxTrustMetaVersion__ None
 * __oxTrustNameFormatted__ None
 * __oxTrustPhoneValue__ None
 * __oxTrustPhotos__ None
 * __oxTrustProfileURL__ None
 * __oxTrustRole__ None
 * __oxTrustTitle__ None
 * __oxTrustUserType__ None
 * __oxTrusthonorificPrefix__ None
 * __oxTrusthonorificSuffix__ None
 * __oxTrustx509Certificate__ None
 * __persistentId__ Persistent id
 * __middleName__ Middle name(s)
 * __nickname__ Casual name of the end-user
 * __preferredUsername__ Shorthand name
 * __profile__ Profile page uri of the person
 * __picture__ Profile picture uri of the person
 * __website__ Web page or blog uri of the person
 * __emailVerified__ True if the email address of the person has been verified; otherwise false
 * __gender__ Gender of the person - either female or male
 * __birthdate__ Birthday of the person, represented as an ISO 8601:2004 [ISO8601â€‘2004] YYYY-MM-DD format
 * __zoneinfo__ time zone database representing the end-user
 * __locale__ Locale of the person, represented as a BCP47 [RFC5646] language tag
 * __phoneNumberVerified__ True if the phone number of the person has been verified, otherwise false
 * __address__ OpenID Connect formatted JSON object representing the address of the person
 * __updatedAt__ Time the information of the person was last updated. Seconds from 1970-01-01T0:0:0Z
 * __preferredLanguage__ Preferred language of the person
 * __role__ Role
 * __secretAnswer__ Secret answer
 * __secretQuestion__ Secret question
 * __seeAlso__ 
 * __sn__ 
 * __cn__ 
 * __transientId__ Transient id
 * __uid__ User id of the person
 * __userPassword__ Password of the person

## Object class gluuSAMLconfig

 * __Description__ 
 * __description__ 
 * __displayName__ 
 * __federationRules__ Track rules for the federation in Gluu SAML configuration. Deprecated as multi-party federation management should move to Jagger
 * __gluuContainerFederation__ SAML trust relationship federation info
 * __gluuEntityId__ Specifies SAML trust relationship entity id
 * __gluuIsFederation__ Used in oxTrust to specify if a SAML trust relationship is a federation. It could also be a website
 * __gluuProfileConfiguration__ SAML trust relationship attribute
 * __gluuReleasedAttribute__ oxTrust reference for the DN of the released attribute
 * __gluuRulesAccepted__ TODO - use unknown for Gluu SAML configuration
 * __gluuSAMLMetaDataFilter__ Metadata filter in SAML trust relationship
 * __gluuSAMLTrustEngine__ SAML trust relationship configuration
 * __gluuSAMLmaxRefreshDelay__ SAML trust relationship refresh time
 * __gluuSAMLspMetaDataFN__ SAML Trust Relationship file location of metadata
 * __gluuSAMLspMetaDataSourceType__ SAML Trust Relationship SP metadata type - file, uri, federation
 * __gluuSAMLspMetaDataURL__ SAML Trust Relationship uri location of metadata
 * __gluuSpecificRelyingPartyConfig__ SAML Trust Relationship configuration
 * __gluuStatus__ Status of the entry, used by many object classes
 * __gluuTrustContact__ oxTrust login page configuration
 * __gluuTrustDeconstruction__ TODO - in use?
 * __gluuValidationLog__ None
 * __gluuValidationStatus__ None
 * __iname__ None
 * __inum__ XRI i-number
 * __o__ 
 * __objectClass__ 
 * __oxAuthPostLogoutRedirectURI__ oxAuth post logout redirect uri
 * __url__ None

## Object class oxAuthClient

 * __Description__ 
 * __associatedPerson__ Reference the DN of a person.
 * __displayName__ 
 * __inum__ XRI i-number (iNum)
 * __oxAuthAppType__ oxAuth app type
 * __oxAuthClientIdIssuedAt__ oxAuth client ID issued at
 * __oxAuthClientSecret__ oxAuth client secret
 * __oxAuthClientSecretExpiresAt__ the date the oxAuth client secret expires
 * __oxAuthClientURI__ oxAuth client uri
 * __oxAuthClientUserGroup__ oxAuth client user group
 * __oxAuthContact__ oxAuth contact
 * __oxAuthDefaultAcrValues__ oxAuth default ACR values
 * __oxAuthDefaultMaxAge__ oxAuth default maximum age
 * __oxAuthFederationId__ oxAuth Federation ID attribute
 * __oxAuthFederationMetadataURI__ oxAuth federation metadata uri attribute
 * __oxAuthGrantType__ oxAuth Grant type
 * __oxAuthIdTokenEncryptedResponseAlg__ oxAuth ID token encrypted response algorithm
 * __oxAuthIdTokenEncryptedResponseEnc__ oxAuth ID token encrypted response encoding
 * __oxAuthIdTokenSignedResponseAlg__ oxAuth ID token signed response algorithm
 * __oxAuthInitiateLoginURI__ oxAuth initiate login uri
 * __oxAuthJwksURI__ uri for the oxAuth JWKs file
 * __oxAuthLogoURI__ uri for the oxAuth logo file
 * __oxAuthPolicyURI__ uri for the oxAuth policy
 * __oxAuthPostLogoutRedirectURI__ uri for the oxAuth post logout redirect
 * __oxAuthRedirectURI__ uri for the oxAuth redirect
 * __oxAuthRegistrationAccessToken__ oxAuth registration access token
 * __oxAuthRequestObjectSigningAlg__ oxAuth request object signing algorithm
 * __oxAuthRequestURI__ oxAuth request uri
 * __oxAuthRequireAuthTime__ oxAuth require authentication time
 * __oxAuthResponseType__ oxAuth response type
 * __oxAuthScope__ oxAuth attribute scope
 * __oxAuthSectorIdentifierURI__ oxAuth sector identifier uri
 * __oxAuthSignedResponseAlg__ oxAuth signed response algorithm
 * __oxAuthSubjectType__ oxAuth subject type
 * __oxAuthTokenEndpointAuthMethod__ oxAuth token endpoint authentication method
 * __oxAuthTosURI__ oxAuth type of service uri
 * __oxAuthTrustedClient__ oxAuth trusted client
 * __oxAuthUserInfoEncryptedResponseAlg__ oxAuth user info encrypted response algorithm
 * __oxAuthUserInfoEncryptedResponseEnc__ oxAuth user info encrypted response encoding
 * __oxLastAccessTime__ Last access time
 * __oxLastLogonTime__ Last logon time

## Object class oxAuthConfiguration

 * __Description__ 
 * __ou__ 
 * __oxAuthConfCustomAuthMethod__ Custom authentication method
 * __oxAuthConfDynamic__ oxAuth dynamic configuration
 * __oxAuthConfErrors__ oxAuth errors configuration
 * __oxAuthConfIdPythonScript__ Custom ID generation
 * __oxAuthConfLdapAuth__ LDAP authentication configuration
 * __oxAuthConfStatic__ oxAuth static configuration
 * __oxAuthConfWebKeys__ oxAuth web keys configuration

## Object class oxAuthCustomScope

 * __Description__ 
 * __defaultScope__ Track the default scope for an custom OAuth2 scope
 * __description__ 
 * __displayName__ 
 * __inum__ XRI i-number (iNum)
 * __oxAuthClaim__ oxAuth attribute claim

## Object class oxAuthFederationMetadata

 * __Description__ 
 * __displayName__ 
 * __inum__ XRI i-number (iNum)
 * __oxAuthFederationMetadataIntervalCheck__ oxAuth Federation metadata interval check attribute
 * __oxAuthFederationOP__ oxAuth Federation OP attribute
 * __oxAuthFederationRP__ oxAuth Federation RP attribute
 * __oxAuthRedirectURI__ oxAuth Redirect uri

## Object class oxAuthFederationOP

 * __Description__ 
 * __displayName__ 
 * __inum__ XRI i-number
 * __oxAuthFederationOpDomain__ oxAuth Federation OP domain attribute
 * __oxAuthFederationOpId__ oxAuth Federation OP ID attribute
 * __oxAuthX509PEM__ oxAuth x509 in PEM format
 * __oxAuthX509URL__ oxAuth x509 uri

## Object class oxAuthFederationRP

 * __Description__ 
 * __displayName__ 
 * __inum__ XRI i-number (iNum)
 * __oxAuthRedirectURI__ oxAuth redirect uri
 * __oxAuthX509PEM__ oxAuth x509 in PEM format
 * __oxAuthX509URL__ oxAuth x509 uri

## Object class oxAuthFederationRequest

 * __Description__ 
 * __displayName__ 
 * __inum__ XRI i-number (iNum)
 * __oxAuthFederationOpDomain__ oxAuth Federation OP domain attribute
 * __oxAuthFederationOpId__ oxAuth Federation OP ID attribute
 * __oxAuthFederationRequestType__ oxAuth Federation request type attribute
 * __oxAuthRedirectURI__ oxAuth redirect uri

## Object class oxAuthFederationTrust

 * __Description__ 
 * __displayName__ 
 * __inum__ XRI i-number
 * __oxAuthFederationId__ oxAuth Federation ID attribute
 * __oxAuthFederationMetadataURI__ oxAuth Federation metadata uri attribute
 * __oxAuthFederationTrustStatus__ oxAuth Federation trust status attribute
 * __oxAuthRedirectURI__ oxAuth redirect uri
 * __oxAuthReleasedScope__ oxAuth released scope attribute
 * __oxAuthSkipAuthorization__ oxAuth skip authorization attribute

## Object class oxAuthSessionId

 * __Description__ 
 * __lastModifiedTime__ timestamp of the last modification
 * __oxAuthAuthenticationTime__ oxAuth authentication time
 * __oxAuthPermissionGranted__ oxAuth permission granted
 * __oxAuthPermissionGrantedMap__ oxAuth permission granted map
 * __oxAuthUserDN__ oxAuth user DN
 * __uniqueIdentifier__ an unique identifier for this object

## Object class oxAuthToken

 * __Description__ 
 * __createTimestamp__ 
 * __oxAuthAuthenticationTime__ oxAuth authentication time
 * __oxAuthAuthorizationCode__ oxAuth authorization code
 * __oxAuthCreation__ oxAuth creation
 * __oxAuthExpiration__ oxAuth expiration
 * __oxAuthGrantId__ oxAuth grant id
 * __oxAuthGrantType__ oxAuth grant type
 * __oxAuthJwtRequest__ oxAuth JWT request
 * __oxAuthNonce__ oxAuth nonce
 * __oxAuthScope__ oxAuth attribute scope
 * __oxAuthTokenCode__ oxAuth token code
 * __oxAuthTokenType__ oxAuth token type
 * __oxAuthUserId__ oxAuth user id
 * __oxAuthenticationLevel__ None
 * __oxAuthenticationMode__ None
 * __uniqueIdentifier__ 

## Object class oxAuthUmaPolicy

 * __Description__ 
 * __description__ 
 * __displayName__ 
 * __inum__ XRI i-number (iNum)
 * __oxAuthUmaScope__ uri reference of scope descriptor
 * __oxPolicyScript__ ox policy script
 * __programmingLanguage__ programming language

## Object class oxAuthUmaRPT

 * __Description__ 
 * __oxAmHost__ AM host
 * __oxAuthAuthenticationTime__ oxAuth authentication time
 * __oxAuthClientId__ oxAuth client ID
 * __oxAuthCreation__ oxAuth creation
 * __oxAuthExpiration__ oxAuth expiration
 * __oxAuthTokenCode__ oxAuth token code
 * __oxAuthUserId__ oxAuth user ID
 * __oxUmaPermission__ ox UMA permission
 * __uniqueIdentifier__ the unique identifier that is in use

## Object class oxAuthUmaResourceSet

 * __Description__ 
 * __displayName__ (user) name that appears on the display
 * __inum__ XRI i-number (iNum)
 * __owner__ 
 * __oxAssociatedClient__ Associate the DN of an OAuth2 client with a person or UMA resource set
 * __oxAuthUmaScope__ uri reference of scope descriptor
 * __oxFaviconImage__ uri for the favicon
 * __oxGroup__ User group
 * __oxId__ oxAuth identifier
 * __oxResource__ Host path
 * __oxRevision__ Revision number
 * __oxType__ ox type

## Object class oxAuthUmaResourceSetPermission

 * __Description__ 
 * __oxAmHost__ AM host
 * __oxAuthExpiration__ oxAuth expiration
 * __oxAuthUmaScope__ uri reference of scope descriptor
 * __oxConfigurationCode__ ox configuration code
 * __oxHost__ ox host
 * __oxResourceSetId__ ox resource set id
 * __oxTicket__ ox ticket

## Object class oxAuthUmaScopeDescription

 * __Description__ 
 * __displayName__ (user) name that appears on the display
 * __inum__ XRI i-number (iNum)
 * __owner__ 
 * __oxFaviconImage__ uri for the favicon
 * __oxIconUrl__ uri for the ox icon
 * __oxId__ ox identifier
 * __oxPolicyRule__ ox policy rule
 * __oxRevision__ ox Revision
 * __oxType__ ox type
 * __oxUrl__ ox uri

## Object class oxEntry

 * __Description__ 
 * __displayName__ (user) name that appears on the display
 * __iname__ None
 * __inum__ XRI i-number (iNum)

## Object class oxLink

 * __Description__ 
 * __description__ oxLink description
 * __oxGuid__ A random string to mark temporary ox tokens
 * __oxLinkCreator__ ox link creator
 * __oxLinkExpirationDate__ ox Link expiration date
 * __oxLinkLinktrack__ ox linktrack link
 * __oxLinkModerated__ is the ox link moderated?
 * __oxLinkModerators__ ox link moderators
 * __oxLinkPending__ pending ox registrations

## Object class oxLiteralNode

 * __Description__ 
 * __literalBinaryValue__ ox literal binary value
 * __literalValue__ ox literal value
 * __organizationalOwner__ ox organizational owner
 * __owner__ ox owner
 * __targetRelationalXdiStatement__ ox TargetRelationalXdiStatement
 * __x__ ox XRI component
 * __xdiStatement__ ox XDI statement
 * __xri__ OX XRI address

## Object class oxNode

 * __Description__ 
 * __organizationalOwner__ ox organizational owner
 * __owner__ ox owner
 * __sourceRelationalXdiStatement__ ox source relational XDI statement
 * __targetRelationalXdiStatement__ ox target relational XDI statement
 * __x__ ox XRI component
 * __xdiStatement__ ox XDI statement
 * __xri__ ox XRI address

## Object class oxProxAccessToken

 * __Description__ 
 * __oxAuthCreation__ oxAuth creation
 * __oxAuthExpiration__ oxAuth expiration
 * __oxProxyAccessToken__ oxProxy access token
 * __oxProxyClientId__ oxProxy client ID

## Object class oxProxClient

 * __Description__ 
 * __displayName__ (user) name that appears on the display
 * __inum__ XRI i-number (iNum)
 * __oxProxyClaimMapping__ oxProxy claim mapping
 * __oxProxyScope__ oxProxy scope
 * __oxProxyToOpClientMapping__ oxProxy client mapping to op client

## Object class oxProxConfiguration

 * __Description__ 
 * __ou__ 
 * __oxProxConf__ oxProxy Configuration
 * __oxScriptDn__ script object DN

## Object class oxProxOp

 * __Description__ 
 * __c__ 
 * __displayName__ (user) name that appears on the display
 * __inum__ XRI i-number (iNum)
 * __l__ 
 * __oxDomain__ ox domain
 * __oxId__ ox identifier
 * __oxX509PEM__ ox X.509 in PEM format
 * __oxX509URL__ ox X.509 uri

## Object class oxPushApplication

 * __Description__ 
 * __displayName__ (user) name that appears on the display
 * __oxId__ ox identifier
 * __oxName__ ox name
 * __oxPushApplicationConf__ oxPush application configuration

## Object class oxPushDevice

 * __Description__ 
 * __oxAuthUserId__ oxAuth user ID
 * __oxId__ ox identifier
 * __oxPushApplication__ oxPush application DN
 * __oxPushDeviceConf__ oxPush device configuration
 * __oxType__ ox type

## Object class oxScript

 * __Description__ 
 * __inum__ XRI i-number (iNum)
 * __oxScript__ Attribute that contains the script (python, java script)
 * __oxScriptType__ Attribute that contains the script type (e.g. python, java script)

## Object class oxTrustConfiguration

 * __Description__ 
 * __ou__ 
 * __oxTrustConfApplication__ oxTrust application configuration

## Object class vdDirectoryView

 * __Description__ 
 * __o__ 

## Object class vdapcontainer

 * __Description__ 
 * __ou__ 

## Object class vdlabel

 * __Description__ 
 * __o__ 

