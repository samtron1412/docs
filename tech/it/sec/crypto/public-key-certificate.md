# Overview

- https://en.wikipedia.org/wiki/Public_key_certificate
- A public key certificate, aka digital certificate or identity
  certificate, is an electronic document used to prove the validity of a
  public key.
- The certificate includes
    + information about the public key
    + information about the identity of its owner (subject)
    + the digital signature of an entity that has verified the
      certificate's contents (issuer)
- If the signature is valid, and the software examining the certificate
  trusts the issuer, then it can use that key to communicate securely
  with the certificate's subject.
- In a typical public-key infrastructure (PKI) scheme, the certificate
  issuer is a certificate authority (CA),[3] usually a company that
  charges customers to issue certificates for them.
    + By contrast, in a web of trust scheme, individuals sign each
      other's keys directly, in a format that performs a similar
      function to a public key certificate.
- The most common format for public key certificates is defined by
  X.509.[4] Because X.509 is very general, the format is further
  constrained by profiles defined for certain use cases, such as Public
  Key Infrastructure (X.509) as defined in RFC 5280.

# Types of certificates

- TLS/SSL server certificate
- TLS/SSL client certificate
- Email certificate
- Self-signed and root certificates
    + Certificate authorities (issuers) self-signs a root certificate,
      and then use it to sign other certificates
    + Self-signed certificates are a certificates with a subject that
      matches its issuer. (most puroses, self-signed certificates are
      worthless, except root certificates)

# X.509: Structure of a certificate

- https://en.wikipedia.org/wiki/X.509

Some common fields:
- Serial Number: Used to uniquely identify the certificate within a CA's systems. In particular this is used to track revocation information.
- Subject: The entity a certificate belongs to: a machine, an individual, or an organization.
- Issuer: The entity that verified the information and signed the certificate.
- Not Before: The earliest time and date on which the certificate is valid. Usually set to a few hours or days prior to the moment the certificate was issued, to avoid clock skew problems.
- Not After: The time and date past which the certificate is no longer valid.
- Key Usage: The valid cryptographic uses of the certificate's public key. Common values include digital signature validation, key encipherment, and certificate signing.
- Extended Key Usage: The applications in which the certificate may be used. Common values include TLS server authentication, email protection, and code signing.
- Public Key: A public key belonging to the certificate subject.
- Signature Algorithm: This contain a hashing algorithm and an encryption algorithm. For example "sha256RSA" where sha256 is the hashing algorithm and RSA is the encryption algorithm.
- Signature: The body of the certificate is hashed (hashing algorithm in "Signature Algorithm" field is used) and then the hash is encrypted (encryption algorithm in the "Signature Algorithm" field is used) with the issuer's private key.

# Public Key Infrastructure

A PKI consists of:
- A certificate authority (CA) that stores, issues and signs the digital certificates;
- A registration authority (RA) which verifies the identity of entities requesting their digital certificates to be stored at the CA;
- A central directory—i.e., a secure location in which keys are stored and indexed;
- A certificate management system managing things like the access to stored certificates or the delivery of the certificates to be issued;
- A certificate policy stating the PKI's requirements concerning its procedures. Its purpose is to allow outsiders to analyze the PKI's trustworthiness.
