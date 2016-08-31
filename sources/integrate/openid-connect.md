# Table of Contents 
[TOC]

# Overview
[OpenID Connect](http://openid.net/connect) ("Connect") is a standard
profile of OAuth2 which defines a protocol to enable a website or mobile
application to send a person to a domain for authentication and required
attributes (e.g. email address, first name, last name, etc.). OpenID Connect
also provides some of the plumbing around authentication to automate how
this happens. If a person is visiting a website for the first time, the
process that OpenID Connect defines is 100% bootstrapable by the
website. This is really critical for Internet scalability. To visit
someone's website, or to send someone an email, you do not need to get
the system administrators involved. Connect provides the same type of
scalable infrastructure for authentication and authorization, and promises to define a base level domain
identification.

## Jargon (taxonomy)

If you are familiar with SAML, there are many parallels in OpenID
Connect, but the jargon (or "taxonomy") is different. For example,
instead of attributes, we have "user claims". Instead of Service
Provider (SP), we have "client". Instead of Identity Provider (IdP), it
is an OpenID Provider (OP).

## Discovery 

The first thing you want to know about any OAuth2 API is where are the
endpoints (i.e. what are the uris where you call the APIs).
OpenID Connect provides a very simple mechanism to accomplish this: 
[OpenID Connect Discovery](http://openid.net/specs/openid-connect-discovery-1_0.html).

In order for an OpenID Connect Relying Party to utilize OpenID Connect
services for an End-User, the RP needs to know where the OpenID Provider is.
OpenID Connect uses WebFinger [WebFinger](http://en.wikipedia.org/wiki/WebFinger)
to locate the OpenID Provider for an End-User.

Once the OpenID Provider has been identified, the configuration information
for the OP is retrieved from a well-known location as a JSON document,
including its OAuth 2.0 endpoint locations.

If you want to try a discovery request, you can make the following
WebFinger request to discover the Issuer location:

```
GET /.well-known/webfinger?resource=https%3A%2F%2Fidp.gluu.org&rel=http%3A%2F%2Fopenid.net%2Fspecs%2Fconnect%2F1.0%2Fissuer HTTP/1.1
Host: idp.gluu.org

HTTP/1.1 200
Content-Type: application/jrd+json

{
    "subject": "https://idp.gluu.org",
    "links": [{
        "rel": "http://openid.net/specs/connect/1.0/issuer",
        "href": "https://idp.gluu.org"
    }]
}
```

Using the Issuer location discovered, the OpenID Provider's configuration information can be retrieved.

The RP makes the following request to the Issuer https://<domain>/.well-known/openid-configuration to obtain its
Configuration information:

```
GET /.well-known/openid-configuration HTTP/1.1
Host: idp.gluu.org

HTTP/1.1 200
Content-Type: application/json

{
    "issuer": "https://idp.gluu.org",
    "authorization_endpoint": "https://idp.gluu.org/oxauth/seam/resource/restv1/oxauth/authorize",
    "token_endpoint": "https://idp.gluu.org/oxauth/seam/resource/restv1/oxauth/token",
    "userinfo_endpoint": "https://idp.gluu.org/oxauth/seam/resource/restv1/oxauth/userinfo",
    "clientinfo_endpoint": "https://idp.gluu.org/oxauth/seam/resource/restv1/oxauth/clientinfo",
    "check_session_iframe": "https://idp.gluu.org/oxauth/opiframe",
    "end_session_endpoint": "https://idp.gluu.org/oxauth/seam/resource/restv1/oxauth/end_session",
    "jwks_uri": "https://idp.gluu.org/oxauth/seam/resource/restv1/oxauth/jwks",
    "registration_endpoint": "https://idp.gluu.org/oxauth/seam/resource/restv1/oxauth/register",
    "validate_token_endpoint": "https://idp.gluu.org/oxauth/seam/resource/restv1/oxauth/validate",
    "federation_metadata_endpoint": "https://idp.gluu.org/oxauth/seam/resource/restv1/oxauth/federationmetadata",
    "federation_endpoint": "https://idp.gluu.org/oxauth/seam/resource/restv1/oxauth/federation",
    "id_generation_endpoint": "https://idp.gluu.org/oxauth/seam/resource/restv1/id",
    "introspection_endpoint": "https://idp.gluu.org/oxauth/seam/resource/restv1/introspection",
    "scopes_supported": [
        "clientinfo",
        "email",
        "openid",
        "profile",
        "address",
        "uma_protection",
        "user_name",
        "uma_authorization",
        "mobile_phone",
        "phone"
    ],
    "response_types_supported": [
        "code",
        "code id_token",
        "token",
        "token id_token",
        "code token",
        "code token id_token",
        "id_token"
    ],
    "grant_types_supported": [
        "authorization_code",
        "implicit",
        "urn:ietf:params:oauth:grant-type:jwt-bearer"
    ],
    "acr_values_supported": ["internal"],
    "auth_level_mapping": {"-1": [["internal"]]},
    "subject_types_supported": [
        "public",
        "pairwise"
    ],
    "userinfo_signing_alg_values_supported": [
        "HS256", "HS384", "HS512",
        "RS256", "RS384", "RS512",
        "ES256", "ES384", "ES512"
    ],
    "userinfo_encryption_alg_values_supported": [
        "RSA1_5", "RSA-OAEP",
        "A128KW", "A256KW"
    ],
    "userinfo_encryption_enc_values_supported": [
        "RSA1_5", "RSA-OAEP",
        "A128KW", "A256KW"
    ],
    "id_token_signing_alg_values_supported": [
        "HS256", "HS384", "HS512",
        "RS256", "RS384", "RS512",
        "ES256", "ES384", "ES512"
    ],
    "id_token_encryption_alg_values_supported": [
        "RSA1_5", "RSA-OAEP",
        "A128KW", "A256KW"
    ],
    "id_token_encryption_enc_values_supported": [
        "A128CBC+HS256", "A256CBC+HS512",
        "A128GCM", "A256GCM"
    ],
    "request_object_signing_alg_values_supported": [
        "none",
        "HS256", "HS384", "HS512",
        "RS256", "RS384", "RS512",
        "ES256", "ES384", "ES512"
    ],
    "request_object_encryption_alg_values_supported": [
        "RSA1_5", "RSA-OAEP",
        "A128KW", "A256KW"
    ],
    "request_object_encryption_enc_values_supported": [
        "A128CBC+HS256", "A256CBC+HS512",
        "A128GCM", "A256GCM"
    ],
    "token_endpoint_auth_methods_supported": [
        "client_secret_basic",
        "client_secret_post",
        "client_secret_jwt",
        "private_key_jwt"
    ],
    "token_endpoint_auth_signing_alg_values_supported": [
        "HS256", "HS384", "HS512",
        "RS256", "RS384", "RS512",
        "ES256", "ES384", "ES512"
    ],
    "display_values_supported": [
        "page",
        "popup"
    ],
    "claim_types_supported": ["normal"],
    "claims_supported": [
        "birthdate",
        "country",
        "name",
        "email",
        "email_verified",
        "given_name",
        "gender",
        "inum",
        "family_name",
        "updated_at",
        "locale",
        "middle_name",
        "nickname",
        "phone_number_verified",
        "picture",
        "preferred_username",
        "profile",
        "zoneinfo",
        "user_name",
        "website"
    ],
    "service_documentation": "http://gluu.org/docs",
    "claims_locales_supported": ["en"],
    "ui_locales_supported": [
        "en", "es"
    ],
    "scope_to_claims_mapping": [
        {"clientinfo": [
            "name",
            "inum"
        ]},
        {"email": [
            "email_verified",
            "email"
        ]},
        {"openid": ["inum"]},
        {"profile": [
            "name",
            "family_name",
            "given_name",
            "middle_name",
            "nickname",
            "preferred_username",
            "profile",
            "picture",
            "website",
            "gender",
            "birthdate",
            "zoneinfo",
            "locale",
            "updated_at"
        ]},
        {"address": [
            "formatted",
            "postal_code",
            "street_address",
            "locality",
            "country",
            "region"
        ]},
        {"uma_protection": []},
        {"user_name": ["user_name"]},
        {"uma_authorization": []},
        {"mobile_phone": ["phone_mobile_number"]},
        {"phone": [
            "phone_number_verified",
            "phone_number"
        ]}
    ],
    "claims_parameter_supported": true,
    "request_parameter_supported": true,
    "request_uri_parameter_supported": true,
    "require_request_uri_registration": false,
    "op_policy_uri": "http://ox.gluu.org/doku.php?id=oxauth:policy",
    "op_tos_uri": "http://ox.gluu.org/doku.php?id=oxauth:tos",
    "http_logout_supported": "true",
    "logout_session_supported": "true"
}
```

The following is an example using the [oxAuth-Client](https://ox.gluu.org/maven/org/xdi/oxauth-client/) lib:

```
String resource = "acct:mike@idp.gluu.org";

OpenIdConnectDiscoveryClient openIdConnectDiscoveryClient = new OpenIdConnectDiscoveryClient(resource);
OpenIdConnectDiscoveryResponse openIdConnectDiscoveryResponse = openIdConnectDiscoveryClient.exec();

.....

OpenIdConfigurationClient client = new OpenIdConfigurationClient(configurationEndpoint);
OpenIdConfigurationResponse response = client.execOpenIdConfiguration();
```

See [org.xdi.oxauth.ws.rs.ConfigurationRestWebServiceHttpTest](https://github.com/GluuFederation/oxAuth/blob/master/Client/src/test/java/org/xdi/oxauth/ws/rs/ConfigurationRestWebServiceHttpTest.java)

## Scopes

In SAML, the IdP releases attributes to the SP. OpenID Connect provides
similar functionality, with more flexibility in case the person needs to
self-approve the release of information from the IdP to the website (or
mobile application). In OAuth2, scopes can be used for various purposes.
OpenID Connect uses OAuth2 scopes to "group" attributes. For example, we
could have a scope called "address" that includes the street, city,
state, and country user claims. By default the Gluu Server defines six
scopes.

![Scopes Screenshot](https://raw.githubusercontent.com/GluuFederation/docs/master/sources/img/oxTrust/admin_oauth2_scope.png)

The Gluu Server administrator can easily add more scopes in the GUI.
Click *Add Scope* and you will be presented with the following screen:

![Add Scopes](https://raw.githubusercontent.com/GluuFederation/docs/master/sources/img/openid_connect/oxtrust_scope_screenshot.png)

You will have the ability to provide a Display Name, Description,
whether or not the scope is provided by default, and the claims that are
included in the scope.

Default Scope needs some further explanation. When a client uses dynamic
client registration, the OpenID Connect specification says that the
`openid` scope should always be released, which contains an identifier
for that person, normally the username. If you want to release another
scope automatically, set the Default Scope to `true` for that scope. You
can always explicitly release a scope to a certain client later on, but
this will require some manual intervention by the domain administrator.

To add more claims, simply click "Add Claim" and you will be presented
with the following screen:

![Add Claims](https://raw.githubusercontent.com/GluuFederation/docs/master/sources/img/oxTrust/admin_oauth2_scopeadd.png)

## Client Registration

A client in OAuth2 could be either a website or mobile application.
OpenID Connect has an API for [Dynamic Client
Registration](http://openid.net/specs/openid-connect-registration-1_0.html)
which efficiently pushes the task to the application developer. If you
do not want to write an application to register your client, there are a
few web pages around that can do the job for you. Gluu publishes the
[oxAuth-RP](https://ce-dev.gluu.org/oxauth-rp) and there is also another in [PHP
RP](http://www.gluu.co/php-sample-rp).

If you cannot get the developer to help themselves, or if your domain
doesn't want to allow dynamic client registration, you can use the
oxTrust admin GUI to manually add trusted clients.

Available **Clients** can be seen by hitting the **Search** button
leaving the search box empty.

![Client List](https://raw.githubusercontent.com/GluuFederation/docs/master/sources/img/oxTrust/admin_oauth2_clientlist.png)

A new client can be added by clicking the **Add Client** link.

![Add Client](https://raw.githubusercontent.com/GluuFederation/docs/master/sources/img/oxTrust/admin_oauth2_addclient.png)

Clicking on the _Add Client_ link allows the Gluu Server administrator
to add a new client. The search box can be used to look up previously
added clients as well. The screenshot below shows the interface to add a
new client.

![Add new client](https://raw.githubusercontent.com/GluuFederation/docs/master/sources/img/oxTrust/admin_oauth2_newclient.png)

* _Client Name:_ This contains the recognizable and unique display name
  of the client. The name of the Client to be presented to the End-User.

* _Client Secret:_ This is the Data Encryption Standard scheme used by
  Confidential Clients to authenticate to the token endpoint. The value for
  the secret can be inserted manually, but it is highly recommended to use
  the Dynamic Client Registration Endpoint. The Gluu oxAuth provides a
  random, generated Client Secret in the Dynamic Client Registration
  procedure.

* _Application Type:_ There are two types of applications, Web and
  Native. The default, if omitted, is web when using the Dynamic
  Client Registration Endpoint. The different configuration for the
   different application types are given below.

	* _Web:_ The Dynamic Client Registration is the default for web. In
    this type the redirect_uri for implicit grant type must be a real
    hostname with HTTPS. This type is not approved any localhost or HTTP.
    The web application uses the authorization code flow for clients which
    can maintain a client secret between the uris and the authorization
    server.

	* _Native:_ Custom uri for Native type application have to follow HTTP
    with localhost. This is suitable for a mobile app which cannot maintain
    the client secret between itself and the authorization server.

* _Pre Authorization:_ The Gluu Server disables this option by default,
  but it is possible to allow pre-authorized Client Applications according to the
  Organization Policy by the Gluu Server administrator.

* _Logo URI:_ The URL of the logo for the client application.
  If present, the server will display this image to the End-User during approval.

* _Client URI:_ The URL of the home page of the client.

* _Policy URI:_ URL that the Relying Party Client provides to the End-User to read about
  the how the profile data will be used. The value of this field must point
  to a valid web page. The OpenID Provider will display this URL to the End-User if it is given.

* _Terms of Service URI:_ URL that the Relying Party Client provides to the End-User to
  read about the Relying Party's terms of service. The value of this field must point to
  a valid web page. The OpenID Provider will display this URL to the End-User if it is given.

* _JWKS URI:_ The URL for the Client's JSON Web Key Set document.
  If the Client signs requests to the Server, it contains the signing key(s) the Server uses to
  validate signatures from the Client. The JWK Set may also contain the Client's encryption keys(s),
  which are used by the Server to encrypt responses to the Client.
  When both signing and encryption keys are made available, a use (Key Use) parameter value is
  required for all keys in the referenced JWK Set to indicate each key's intended usage.
  Although some algorithms allow the same key to be used for both signatures and encryption,
  doing so is NOT RECOMMENDED, as it is less secure.
  
* _JWKS:_ Client's JSON Web Key Set document, passed by value.
  The semantics of the jwks parameter are the same as the jwks_uri parameter, other than that the
  JWK Set is passed by value, rather than by reference.
  This parameter is intended only to be used by Clients that, for some reason, are unable to use
  the jwks_uri parameter, for instance, by native applications that might not have a location to
  host the contents of the JWK Set.
  If a Client can use jwks_uri, it must not use jwks. One significant downside of jwks is that it
  does not enable key rotation (which jwks_uri does).
  The jwks_uri and jwks parameters MUST NOT be used together.

* _Sector Identifier URI:_ URL using the https scheme to be used in calculating Pseudonymous
  Identifiers by the OP.
  The URL references a file with a single JSON array of redirect_uri values.
  Providers that use pairwise sub (subject) values should utilize the sector_identifier_uri
  value provided in the Subject Identifier calculation for pairwise identifiers.
  
* _Subject Type:_ The subject type requested for responses to this Client.
  The subject_types_supported Discovery parameter contains a list of the
  supported subject_type values for this server. Valid types include pairwise and public.

* _JWS alg Algorithm for signing the ID Token:_ JWS alg algorithm for signing the ID Token issued to this Client.
  See [Algorithms section](#algorithm) for options.

* _JWE alg Algorithm for encrypting the ID Token:_ JWE alg algorithm for encrypting the ID Token issued to this Client.
  See [Algorithms section](#algorithm) for options.

* _JWE enc Algorithm for encrypting the ID Token:_ JWE enc algorithm for encrypting the ID Token issued to this Client.
  See [Algorithms section](#algorithm) for options.

* _JWS alg Algorithm for signing the UserInfo Responses:_ JWS alg algorithm for signing UserInfo Responses.
  If this is specified, the response will be JWT serialized, and signed using JWS.
  The default, if omitted, is for the UserInfo Response to return the Claims as a UTF-8 encoded JSON object
  using the application/json content-type.
  See [Algorithms section](#algorithm) for options.

* _JWS alg Algorithm for encrypting the UserInfo Responses:_  JWE alg algorithm for encrypting UserInfo Responses.
  See [Algorithms section](#algorithm) for options.

* _JWE enc Algorithm for encrypting the UserInfo Responses:_ JWE enc algorithm for encrypting UserInfo Responses. 
  See [Algorithms section](#algorithm) for options.

* _JWS alg Algorithm for signing Request Objects:_ JWS alg algorithm used for signing Request Objects sent to the OP.
  This algorithm is used both when the Request Object is passed by value (using the request parameter) and when it is
  passed by reference (using the request_uri parameter).
  The default, if omitted, is that any algorithm supported by the OP and the RP can be used.
  The value none can be used.
  See [Algorithms section](#algorithm) for options.

* _JWE alg Algorithm for encrypting Request Objects:_ JWE alg algorithm the RP is declaring that it use for
  encrypting Request Objects sent to the OP.
  See [Algorithms section](#algorithm) for options.

* _JWE enc Algorithm for encrypting Request Objects:_ JWE enc algorithm the RP is declaring that it may use for
  encrypting Request Objects sent to the OP.
  See [Algorithms section](#algorithm) for options.

* _Authentication method for the Token Endpoint:_ Requested Client Authentication method for the Token Endpoint.
  The options are client_secret_post, client_secret_basic, client_secret_jwt, private_key_jwt, and none.
  If omitted, the default is client_secret_basic, the HTTP Basic Authentication Scheme.

* _JWS alg Algorithm for Authentication method to Token Endpoint:_ JWS alg algorithm used for signing the JWT
  used to authenticate the Client at the Token Endpoint for the private_key_jwt and client_secret_jwt
  authentication methods. The value none cannot be used.
  The default, if omitted, is that any algorithm supported by the OP and the RP can be used.
  See [Algorithms section](#algorithm) for options.

* _Default Maximum Authentication Age:_ Specifies that the End-User must be actively authenticated if the End-User was
  authenticated longer ago than the specified number of seconds.
  If omitted, no default Maximum Authentication Age is specified.

* _Require Auth Time:_ Specifies whether the auth_time Claim in the ID Token is required.
  If omitted, the default value is false.

* _Persist Client Authorizations*:_ Specifies whether to persist user authorizations.

* _Initiate Login URI:_ URI using the https scheme that a third party can use to initiate a login by the RP.

* _Request URIs:_ Array of request_uri values that are pre-registered by the RP for use at the OP.
   The Server cache the contents of the files referenced by these URIs and not retrieve them at
   the time they are used in a request.
   If the contents of the request file could ever change, these URI values should include the base64url
   encoded SHA-256 hash value of the file contents referenced by the URI as the value of the URI fragment.
   If the fragment value used for a URI changes, that signals the server that its cached value for that URI
   with the old fragment value is no longer valid. 

* _Logout URIs:_ Redirect logout URLs supplied by the RP to which it can request that the End-User's
  User Agent be redirected using the post_logout_redirect_uri parameter after a logout has been performed.

* _Logout Session Required*:_ Specifies whether the RP requires that a sid (session ID) query parameter
  be included to identify the RP session at the OP when the logout_uri is used.
  If omitted, the default value is false.

* _Client Secret Expires:_ Time at which the client will expire or 0 if it will not expire.

**Buttons at the bottom**

* _Add Login URI:_ This option can be used to add the login URL.
![Add Login URI](https://raw.githubusercontent.com/GluuFederation/docs/master/sources/img/oxTrust/admin_oauth_loginuri.png)

* _Add Scopes:_ This option can be used to add the required scopes in the Gluu Server.
![Add Scopes](https://raw.githubusercontent.com/GluuFederation/docs/master/sources/img/oxTrust/admin_oauth2_addscope.png)

  The available scopes can be listed by hitting the *Search* button, and
  keeping the search phrase blank. Furthermore, from this the Gluu Server
  administrator can select the required scopes.

* _Add Response Type:_ There are three types of responses in the Gluu
  Server and they are Code, Token and ID Token. The Gluu Server
  Administrator can select all of them for testing purposes.
![Response Type](https://raw.githubusercontent.com/GluuFederation/docs/master/sources/img/oxTrust/admin_oauth2_response.png)

* _Add Grant Type:_ There are 3 grant type available in this option `authorization_code, implicit, refresh_token`
![Grant Type](https://raw.githubusercontent.com/GluuFederation/docs/master/sources/img/oxTrust/admin_oauth2_grants.png)

* _Add Contact:_ Use this option to add the email address for the Client contact

* _Add Default ACR value:_ Use this option to define the default ACR Value

* _Add Request URI:_ Use this option to add the Request URI

### Algorithm
oxAuth supports various types of signature and encryption
algorithms for authorizing request parameter passing, ID token signature
and encryption, signing return responses, Encrypt User Info Endpoints
etc.

**Note:** It is a good practice to implement ID Token Signatures with the RSA
SHA-256 algorithm (algorithm value RS256). Additionally, oxAuth also
supports other algorithms that are listed below.

_Available Signature Algorithms:_ none, HS256, HS384, HS512, RS256, RS384, RS512, ES256, ES384, ES512.

_Encryption, Key Encryption Algorithms:_ RSA1_5, RSA-OAEP, A128KW, A256KW.

_Block Encryption Algorithms:_ A128CBC+HS256, A256CBC+HS612, A128GCM, A256GCM,

### Custom Client Registration

Using interception scripts you can customize client registration
behavior. For example, by default oxAuth allows new clients to access to
default scopes only. With a custom client registration interception
script it is possible to allow access to more scopes. For instance, we
can use `redirect_uri` to determine if we need to allow access to
additional scopes or not.

To access the interface for custom scripts in oxTrust, navigate to
Configuration --> Custom Scripts --> Custom Client Registration.

Take a look at our [example client registration
script](../customize/sample-client-registration-script.py)
for further reference.

### Search clients
![](http://www.gluu.org/docs/img/openid_connect/oxtrust_search_clients.png "Screenshot of oxTrust browse / search clients")

### View client

![](http://www.gluu.org/docs/img/openid_connect/oxtrust_view_client.png "Screenshot of oxTrust view client")

## Session management

Logout is a catch-22. There is no perfect answer to logout that
satisfies all the requirements of all the domains on the Internet. For
example, large OpenID Providers, like Google, need a totally stateless
implementation--Google cannot track sessions on the server side for
every browser on the Internet. But in smaller domains, server side
logout functionality can be a convenient solution to cleaning up
resources.

The OpenID Connect [Session
Management](http://openid.net/specs/openid-connect-session-1_0.html) is
still marked as draft, and new mechanisms for logout are in the works.
The current specification requires JavaScript to detect that the session
has been ended in the browser. It works... unless the tab with the
JavaScript happens to be closed when the logout event happens on another
tab. Also, inserting JavaScript into every page is not feasible for some
applications. A new proposal is under discussion where the OpenID
Connect logout API would return `IMG` HTML tags to the browser with the
logout callbacks of the clients. This way, the browser could call the
logout uris (not the server).

The Gluu Server is very flexible, and supports both server side session
management, and stateless session management. For server side business
logout, the domain admin can use Custom Logout scripts. This can be
useful to clean up sessions in a legacy SSO system (i.e. SiteMinder), or
perhaps in a portal.

The key for logout is to understand the limitations of logout, and to
test the use cases that are important to you, so you will not be
surprised by the behavior when you put your application into production.

## Testing with oxAuth RP

  - Go to https://seed.gluu.org/oxauth-rp
  - Or deploy `oxAuth-rp.war`

### OpenID Connect Discovery

  - Enter an identifier, for example: https://seed.gluu.org or acct:mike@seed.gluu.org
  - Click submit.

![](http://www.gluu.org/docs/img/oxAuth-RP/openidconnectdiscovery.png "Screenshot of oxAuth-RP OpenID Connect Discovery")

### Dynamic Client Registration

![](http://www.gluu.org/docs/img/oxAuth-RP/dynamicclientregistration.png "Screenshot of oxAuth-RP Dynamic Client Registration")

#### Client Read

![](http://www.gluu.org/docs/img/oxAuth-RP/clientread.png "Screenshot of oxAuth-RP Client Read")


### Authorization Endpoint

#### Request Authorization and receive the Authorization Code and ID Token

  - Go to https://seed.gluu.org/oxauth-rp
  - Enter the Authorization Endpoint (eg: https://seed.gluu.org/oxauth/seam/resource/restv1/oxauth/authorize)
  - Select the Response Types: CODE and ID_TOKEN
  - Enter the Client ID (eg: @!EDFB.879F.2DAE.D95A!0001!0442.B31E!0008!A2DA.C10F)
  - Select the desired scopes: OpenID is mandatory, profile, address,
    email and phone are optional.
  - Enter a Redirect uri, e.g. https://seed.gluu.org/oxauth-rp/home.seam
  - Optionally enter a state value.
  - Click submit.

![](http://www.gluu.org/docs/img/oxAuth-RP/requestauthorizationcodegrant.png "Screenshot of oxAuth-RP Authorization Endpoint")

#### Request Access Token using the Authorization Code

  - Once redirected back to https://seed.gluu.org/oxauth-rp
  - Enter the Token Endpoint (eg: https://seed.gluu.org/oxauth/seam/resource/restv1/oxauth/token)
  - Select the Grant Type: AUTHORIZATION_CODE
  - Enter the Client ID.
  - Enter the Client Secret.
  - Enter the Code received from the previous request
  - Enter the Redirect uri, e.g. https://seed.gluu.org/oxauth-rp/home.seam
  - Enter the scopes: OpenID profile address email phone.
  - Click submit.

![](http://www.gluu.org/docs/img/oxAuth-RP/requestaccesstokenwithauthorizationcode.png "Screenshot of oxAuth-RP Token Endpoint")

#### Request new Access Token using the Refresh Token

  - Go to https://seed.gluu.org/oxauth-rp
  - Enter the Token Endpoint (https://seed.gluu.org/oxauth/seam/resource/restv1/oxauth/token)
  - Select the Grant Type: REFRESH_TOKEN
  - Enter the Client ID.
  - Enter the Client Secret.
  - Enter the Refresh Token received in a previous request.
  - Click submit.

![](http://www.gluu.org/docs/img/oxAuth-RP/refreshtoken.png "Screenshot of oxAuth-RP Refresh Token")


### UserInfo Endpoint

![](http://www.gluu.org/docs/img/oxAuth-RP/userinfoendpoint.png "Screenshot of oxAuth-RP User Info Endpoint")

### OpenID Connect Session Management

#### End Session Endpoint

![](http://www.gluu.org/docs/img/oxAuth-RP/endsession.png "Screenshot of oxAuth-RP End Session Endpoint")

#### Check Session iFrame

![](http://www.gluu.org/docs/img/oxAuth-RP/checksession.png "Screenshot of oxAuth-RP Check Session iFrame")

# oAuth 2 Grants

There are two additional flows that the Gluu Server supports for user
and client authentication, which are not part of the OpenID Connect
specification. The flows are explained in the following page.

* [oAuth 2 Grants](./oauth2grants.md)
