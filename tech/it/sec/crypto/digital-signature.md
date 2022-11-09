# Overview

- https://en.wikipedia.org/wiki/Digital_signature
- A digital signature is a mathematical scheme for verifying the
  authenticity of digital messages.
- A digital signature scheme typically consists of three algorithms:
    + A key generation algorithm that selects a private key uniformly at
      random from a set of possible private keys. The algorithm outputs
      the private key and a corresponding public key.
    + A signing algorithm that, given a message and a private key,
      produces a signature.
    + A signature verifying algorithm that, given the message, public
      key and signature, either accepts or rejects the message's claim
      to authenticity.
