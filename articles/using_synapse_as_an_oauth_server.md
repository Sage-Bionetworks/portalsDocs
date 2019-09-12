---
title: "Using Synapse as an OAuth 2.0 Server"
layout: article
excerpt: Follow these steps to register an OAuth Client and link it to Synapse.
category: howto
---

<style>
#image {
    width: 100%;
}
#imageSmall {
    width: 40%;
}
</style>


# Registering and linking an OAuth 2.0 Client
Synapse implements the [OpenID Connect](https://openid.net/specs/openid-connect-core-1_0.html) protocol, which is an extension of OAuth 2.0.  The Open ID Connect endpoint is `https://repo-prod.prod.sagebase.org/auth/v1`, and the Open ID Configuration (aka the "discovery document") is published in the standard location: [https://repo-prod.prod.sagebase.org/auth/v1/.well-known/openid-configuration](https://repo-prod.prod.sagebase.org/auth/v1/.well-known/openid-configuration).

## Create an OAuth 2.0 Client
You can create a client programmatically as follows:


##### Python

```python
import synapseclient
import json
syn = synapseclient.login()

clientMetaData = {
  'client_name': 'Your client name',
  'redirect_uris': [
    'https://yourhost.com/user/login'
  ],
  'client_uri': 'https://yourhost.com/index.html',
  'policy_uri': 'https://yourhost.com/policy',
  'tos_uri': 'https://yourhost.com/terms_of_service',
  'userinfo_signed_response_alg': 'RS256'
}

clientMetaData = syn.restPOST(uri='/oauth2/client', endpoint=syn.authEndpoint, body=json.dumps(clientMetaData))

client_id = clientMetaData['client_id']

clientIdAndSecret = syn.restPOST(uri='/oauth2/client/secret/'+client_id, endpoint=syn.authEndpoint, body='')

print(clientIdAndSecret)

```

The client URI, policy URI, and terms of service URI are optional, as is the `userinfo_signed_response_alg` parameter.  Further, you can optionally include a `sector_identifier_uri` parameter.  This is an advanced feature described [here](https://openid.net/specs/openid-connect-registration-1_0.html#SectorIdentifierValidation) and is relevant if the client uses multiple hosts because Synapse only returns `pairwise` subject values to its OAuth clients.


The returned `client_id` and `client_secret` will be needed later when getting an access token.  The secret is only returned once.  (Synapse does not keep it.)  If lost, you can generate a new secret but the previous one will be invalidated.

You can retrieve, update, and delete your client programmatically as well:

```python
clientMetaData = syn.restGET(uri='/oauth2/client/'+client_id, endpoint=syn.authEndpoint)

clientMetaData['policy_uri'] = 'https://yourhost.com/updated_policy'

clientMetaData = syn.restPUT(uri='/oauth2/client/'+client_id, endpoint=syn.authEndpoint, clientMetaData)

syn.restDELETE(uri='/oauth2/client/'+client_id, endpoint=syn.authEndpoint)

```

To login via Synapse your client should redirect the browser from your application to `https://signing.synapse.org`, with the standard OAuth 2.0 request parameters:

- `client_id`=<your client id>
- `scope`=`openid`
- `redirect_uri`=<the redirect uri registered with your client>
- `response_type`=`code`
- `state`=<any state you want returned>
- `nonce`=<some string to be returned in the ID token>
- `claims`=<a JSON object>

Synapse supports the `claims` request parameter, a JSON document containing the details of the user identity information you would like returned, as described [here](https://openid.net/specs/openid-connect-core-1_0.html#ClaimsParameter).  The list of supported claims is given here TBD.  For most claims the value to include in the JSON document is `null`.  The exception is the `team` claim, for which you provide the IDs of one or more teams, the membership of which you wish to inquire about.  Synapse will return the IDs of the subset of the given list of teams to which the user belongs.  Here is an example of a claims parameter JSON object:

```
 {
   "id_token":
    {
     "given_name": null,
     "family_name": null,
     "is_certified": null,
     "team": {"values":["273957", "3385814"]}
    },
   "userinfo":
    {
     "given_name": null,
     "family_name": null,
     "is_certified": null,
     "team": {"values":["273957", "3385814"]}
    }
  }
```

Following the user's consent, Synapse will redirect back to your specified redirect URI with an authorization code and your 'state' data.  You can then exchange the authorization code for a ID token and access token in the standard way.  Here is an example using cUrl:

```
curl -H "Authorization:Basic XXXXXXXXXXX" -X POST "https://repo-prod.prod.sagebase.org/auth/v1/oauth2/token?grant_type=authorization_code&redirect_uri=<redirect URI>&code=<authorization code>

```
where `<redirect URI>` is as before and `<authorization code>` is the value returned to your application by Synapse.  The request is authorized using the `client_id` and `client_secret` provided by Synapse, encoded in the header in the standard way: joined with a ':' separator and base 64 encoded.  Synapse responds with an ID Token and access token:


```
{
  "id_token": ...,
  "access_token": ...
}
```

Each token is a signed JSON Web Token.  The public key(s) used to verify the token signatures are available at the JSON Web Key Set (jwks) URL listed in the OpenID Configuration document.  The ID Token contains the requested user identity information.  The access token can be used to authorize future requests.  To get an updated ID Token using the access token as authorization, send a request to the `userinfo` endpoint:

```
curl -H "Authorization:Bearer <access token>" https://repo-prod.prod.sagebase.org/auth/v1/oauth2/userinfo

```

where <access token> is the value returned above.  If the `'userinfo_signed_response_alg': 'RS256'` option was included in the client registration then the result will be returned as another signed JSON Web Token, otherwise a simple JSON object will be returned.




