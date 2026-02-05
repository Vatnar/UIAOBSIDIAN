Resource owner: you.
Client: Application.
Authorisation Server: Where your user lives.
Resource server: API with your data.
Access Token: Security token for API.
Refresh token. Token to refresh the security token.
1. 
Website sends alice to
GET /authorize
response_type
client_id
redirect_uri
scope what permissions
state hinder xss

2.
 Callback
 code
 state
 Authorization Code: a short-lived temporary code the cleint gives the Authorization server in change for an access token.

3. POST /token
grant_type : grant access (authorization_code) show consent from alice
code
client_id, who is the server
client_secret, is it actually the server

4. Token response
access_token
token_type
expires_in
refresh_token
scope

A bearer Token is an opaque string, not intended to have any meaning to clients using it

5. API call
GET /api/pjhotos, authorization bearer token.

Client Credentials
Client credentials are used as an authoriation grant typically when the client is acting on its own behalf. Or is requesting access to protected resources between on an authorization previously arrranged.

AS: Authoirzation server.
RS: Resource server
AT Access token
RT refresh token
JWT Json web tokens


Opaque tokens - reference tokens.
JWT (self contained tokens): 
A bearer token is an opaque string, not intended to have any meaning to clients using it.

Token introspection
POST /token_info
Token revocation
POST /revoke
mark as expired in the database. RS will know when it does introspection

JWT (self contained tokens) short lifetime.

Refresh token
POST /token
User doesnt have to authorize again
Refresh token is bound to the client
Not used with client credentials

Consent
Central part of the specification
but, for instance google, not consenst screen for every app.

What about authentication
OIDC = OpenID Connect

PKCE
Proof key code exchange
/authorize
/callback
man in the middle.

generate code verifier, send with /authorize (code challenge) a hash of the code verifier
saved at server side, (the challenge).
when we do the token, we send the code verifier, so that the server can hash it to check to verify

Client Assertions & public/private keys
shared secrets? no thank you.
use private_key_jwt instead, instead of sending shared secret, we send a client assertion. Just a jwt, save a public key for the user. 

FAPI 2.0
financial grade api, now FAPI

high value use-cases
3 parts.
FAPI 2.0 Security Profile
FAPI 2.0 Message Sigining
FAPI 2.0 Attacker Model


More OAuth snacks
API to API calls - Token Exchange
API we call might need data from another api. 
AT cant be forwarded
- might not contain the right claims
- need to know the original source of the call

