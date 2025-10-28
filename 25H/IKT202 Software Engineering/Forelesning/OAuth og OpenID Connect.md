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