[TOC]

# Overview


# Salted Password Hashing - Doing it Right
## Password hashing
The general workflow for account registration and authentication in a hash-based account system is as follows:

1. The user creates an account.
2. Their password is hashed and stored in the database. At no point is the plain-text (unencrypted) password ever written to the hard drive.
3. When the user attempts to login, the hash of the password they entered is checked against the hash of their real password (retrieved from the database).
4. If the hashes match, the user is granted access. If not, the user is told they entered invalid login credentials.
5. Steps 3 and 4 repeat everytime someone tries to login to their account.

In step 4, never tell the user if it was the username or password they got wrong. Always display a generic message like "Invalid username or password." This prevents attackers from enumerating valid usernames without knowing their passwords.

Only cryptographic hash functions may be used to implement password hashing. Hash functions like `SHA256`, `SHA512`, `RipeMD`, and `WHIRLPOOL` are cryptographic hash functions.

## How hashes are cracked
### Dictionary and Brute force attacks
A dictionary attack uses a file containing words, phrases, common passwords, and other strings that are likely to be used as a password. These dictionary files are constructed by extracting words from large bodies of text, and even from real databases of passwords. Adding "leet speak".

A brute-force attack tries every possible combination of characters up to a given length.

### Lookup tables
Pre-compute the hashes of the passwords in a password dictionary and store them, and their corresponding password, in a lookup table data structure.

### Reverse lookup tables


### [Rainbow tables](https://en.wikipedia.org/wiki/Rainbow_table)
Like lookup tables, except that they sacrifice hash cracking speed to make the lookup tables smaller.

## Adding Salt

## Ineffective hashing methods


## How to hash properly



