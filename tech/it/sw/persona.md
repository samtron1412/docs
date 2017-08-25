[TOC]

#Persona
Simple, privacy-sensitive single sign-in: let your users sign into your website with their email address, and free yourself from password management.

Built on an *open, decentralized protocol*, that's designed to allow *direct integration into browsers* and *native support by email providers*.

[Developer page](https://developer.mozilla.org/en-US/Persona)

[Mozilla Persona](https://login.persona.org/)

[Privacy](https://login.persona.org/en/privacy)

[Term of Service](https://login.persona.org/en/tos)

[Quick Setup Persona in your website](https://developer.mozilla.org/en-US/Persona/Quick_Setup)

##Features

###Eliminates site-specific passwords.
Built on top of public-key cryptography for logging in to websites.The user's browser generates a cryptographic affirmation of identity that expires after a few minutes and is only valid on one site.

###Users can use any email address.
- Benefits for the user
    + Users already know their email addresses. They don't have to learn a new potentially confusing system.
    + The email addresses carefully capture the idea of *someone@some-context*. This makes it easier for users to keep their identities *@work*, *@home*, or *@school* separate. This differs from the trend of linking together many accounts through real identity, single-account policies on social networks like Google+ and Facebook.
    + Email can be self-organized or delegated to other providers, giving users control of their identity. This ability is greatly diminished when one must consolidate many accounts into one identity.
- Advantages for developers
    + Email addresses let developers communicate directly with users.
    + Persona provides email addresses to websites automatically when a user logs in, eliminating the need for additional post-signup forms.
    + Many login systems treat email addresses as unique keys, so there is no lock-in to Persona and it can be integrated with existing access systems. Any user who has an email address can access content almost immediately.

###Different from other providers of single sign-on
-  Persona allows users to keep their work, school, and social identities separate by using email addresses as a unique identifier rather than real names. Because of this anonymity you are guaranteed an extra layer of identity and network protection that most social networks do not have.
-  Persona also takes a new approach to protecting user privacy by placing *the user's browser in the center of the authentication process*. The browser obtains credentials provided by the user's email, then presents these credentials to a website. The email provider cannot track the user, but *sites can still have confidence in the identity of the user by cryptographically verifying the credentials*. Most other systems, even distributed systems like OpenID, require sites to connect to central networks before allowing a user to log in.

##Get started
Setup a website use Persona like an authentication system. [Quick Setup](https://developer.mozilla.org/en-US/Persona/Quick_Setup)

##The Persona project

###Glossary

####"Persona" vs "BrowserID"
*Persona* is a complete implementation of a new, distributed login system from Mozilla.

*BrowserID* is the open protocol that governs how Persona works.

####Identity Provider (IdP)
Services which issues credentials to their users.

Email providers can become IdP for their users by adding support for the BrowserID authentication protocol to their services. If an email provider doesn't support Persona, Mozilla operates a fallback IdP at [login.persona.org](https://login.persona.org/). 

####login.persona.org
A fallback IdP run by the Identity Team at Mozilla.

####Relying Party (RP)
Any website, application, or service that allows users to log in via Persona.

###FAQ

####Persona vs OpenID
Similar goals and a similar architecture. Both systems reduce the number of passwords that a users needs, and both are designed to be decentralized. This means that any domain can present itself as an Identity Provider without relying on a central authority.

**Persona is easier for users**
>Persona identifies users based on email addresses, which users already know, understand, and naturally associate with online identities. With OpenID, users are forced to learn a new username: an unintuitive URL.

**Persona is easier for developer**
>Persona has a [simple API](https://developer.mozilla.org/en-US/docs/Web/API/navigator.id) that only takes an afternoon to get started with.

**Persona better products user privacy**
>By design, OpenID allows Identity Providers to track their users around the web: whenever a user logs into a website, their browser gets redirected from that site to the user's Identity Provider, and then back to the site that the user requested. These redirects fully expose to the Identity Provider where the user is going.

>In contrast, the BrowserID protocol never leaks tracking information back to the Identity Provider. Rather, it behaves similarly to an ID card: users obtain signed credentials from their Identity Providers which can be presented to websites as a proof of identity. Websites can check the validity of these credentials without ever revealing a user's identity to their identity provider.

####Why does Persona require JavaScript?
JavaScript is actually used to enhance user privacy, as it allows the browser to perform cryptographic operations completely on the client side. By doing these operations on the client, Persona avoids the need to store secret keys anywhere other than in the user's own browser.

###BrowserID protocol overview

####Actors
Three actors:

- **Users**: The actual people that want to sign into websites using Persona.
- **Relying Parties(RPs)**: Websites that want to let users sign in using Persona.
- **Identity Provider(IdPs)**: Domain that can issue Persona-compatible identity certificates to their users.

Persona and the BrowserID protocol use email addresses as identities, so it's natural for email providers to become IdPs.

Mozilla operates a fallback IdP so that users can use any email address with Persona, even one with a specific domain that isn't an IdP itself.

####Protocol Steps
There are three distinct steps in the protocol:

1. User Certificate Provisioning
2. Assertion Generation
3. Assertion Verification

As a prerequisite, the user should have an active identity (email address) that they wish to use when logging in to websites. The protocol does not require that IdP-backed identities are SMTP-routable, but it does require that identities follow the user@domain format.

#####User Certificate Provisioning

#####Assertion Generation

#####Assertion Verification

###Cryptography


