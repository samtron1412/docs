# Overview

- https://en.wikipedia.org/wiki/OpenID
- https://auth0.com/docs/authenticate/protocols/openid-connect-protocol
- https://openid.net/connect/
- https://docs.microsoft.com/en-us/azure/active-directory/develop/v2-protocols-oidc
- https://developers.google.com/identity/protocols/oauth2/openid-connect

# Specifications

- https://openid.net/developers/specs/

## OpenID Connect core 1.0

- https://openid.net/specs/openid-connect-core-1_0.html

# ID Token validation steps

- https://openid.net/specs/openid-connect-core-1_0.html#IDTokenValidation
- https://connect2id.com/blog/how-to-validate-an-openid-connect-id-token
- https://bitbucket.org/b_c/jose4j/wiki/JWT%20Examples#markdown-header-using-an-https-jwks-endpoint

## Clients

```
General steps

1. Verify that the ID token is properly signed by the
   issuer. Google-issued tokens are signed using one of the certificates
   found at the URI specified in the jwks_uri metadata value of the
   Discovery document.
2. Verify that the value of the iss claim in the ID token is equal to
   https://accounts.google.com or accounts.google.com.
3. Verify that the value of the aud claim in the ID token is equal to
   your app's client ID.
4. Verify that the expiry time (exp claim) of the ID token has not
   passed.
5. If you specified a hd parameter value in the request, verify that the
   ID token has a hd claim that matches an accepted domain associated
   with a Google Cloud organization. (nonce)
```

- Other back-end services can skip the step 5 for nonce.

## Libraries

- https://bitbucket.org/b_c/jose4j/wiki/Home
- https://github.com/auth0/java-jwt
- https://github.com/jwtk/jjwt
    + https://www.viralpatel.net/java-create-validate-jwt-token/
- Nimbus-JOSE-JWT
    + https://bitbucket.org/connect2id/nimbus-jose-jwt/src/master/
    + https://connect2id.com/products/nimbus-jose-jwt
- OIDC debugger
    + https://oidcdebugger.com/
