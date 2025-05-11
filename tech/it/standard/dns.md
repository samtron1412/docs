[TOC]

# Overview

- https://en.wikipedia.org/wiki/Domain_Name_System
- https://stackoverflow.com/questions/11887334/understanding-the-dns-lookup-mechanism

The Domain Name System (DNS) is a hierarchical decentralized naming
system for computers, services, or any resource connected to the
Internet or a private network.

It translates more readily memorized domain names to the numerical IP
addresses needed for the purpose of locating and identifying computer
services and devices with the underlying network protocols.

Standards
- https://datatracker.ietf.org/doc/html/rfc1034
- https://datatracker.ietf.org/doc/html/rfc1035
- Security extension standards
    + https://datatracker.ietf.org/doc/html/rfc4033
    + https://datatracker.ietf.org/doc/html/rfc4034
    + https://datatracker.ietf.org/doc/html/rfc4035
    + https://datatracker.ietf.org/doc/html/rfc7858
    + https://datatracker.ietf.org/doc/html/rfc8484

+ Domain Name Registration: buy domain names from registrar
+ Domain Name System
    * Nameservers: which servers are responsible for domain names
      record requests.
        - Name servers are servers in the Domain Name System (DNS) that
          help to translate domain names into the IP addresses that
          computers use to communicate with one another.
        - Root nameservers `.`: is represented as a dot, and they store
          the information of the Top Level Domains (TLD's).
        - TLD nameservers: store the information for all the domain
          names that share a common domain extension such as .com, .net.
        - Authoritative nameserver: store information of specific
          domains.
    * Recursive DNS resolving algorithm.
        - The algorithm to resolve the domain names to IP addresses
          recursively.
    * DNS Zone
        - A distinct part of the domain namespace which is delegated to
          a legal entity (a person, organization or company) who are
          responsible for maintaining that DNS zone.
        - E.g., amazon.com, corp.amazon.com, etc.
    * DNS (Resource) Records  (RR)
        - DNS record is an object in a hosted zone that you use to define
          how you want to route traffic for the domain or a subdomain.
        - DNS zone records:
            + Domain
            + Time to live
                * how long a nameserver is supposed to cache the DNS
                  answer before it expires and a new query needs to be
                  done.
                * negative TTL: records do not exist
            + Class
            + Type
                * https://en.wikipedia.org/wiki/List_of_DNS_record_types
                * A: tie the domain or subdomain to an IPv4 address
                * AAAA (quad A): tie the domain or subdomain to an IPv6 address.
                * CNAME: tie the domain or subdomain to another domain or subdomain
                * PTR: (pointer) is used in the reverse DNS mapping from
                  IP address to a domain. (reverse of A records)
                    - IP: 1.2.3.4
                    - PTR: 4.3.2.1.in-addr.arpa (`<IP-in-reverse-order>.in-addr.arpa`)
                * NS: the nameserver record indicates which DNS server
                  is authoritative for the domain.
                    - A domain will often have multiple NS records which
                      can indicate primary and backup name servers for
                      the domain.
                * MX: define how mail is handled for your domain,
                  including: priority (lower number is higher
                  priority) and answering mail server domain name.
                * TXT: associate text data with your domain. Is used
                  for SPF or DKIM.
                * SOA (Start of Authority) records: are configured by the
                  DNS service provider automatically, so we don't need to
                  configure these.
                    - Mandatory record in all zones
                    - The fields includes the primary name server, the
                      email of the administrator, the domain number and
                      timers for refreshing the zone.
            + Content
- DNS delegation
    + DNS delegation is when a hosted zone delegates authority over a
      part of its namespace to one or more other hosted zones.
    + Delegation is done by defining an NS record in the parent hosted
      zone that points to nameservers of another hosted zone. This
      allows service teams to manage their own part of a DNS space.

# Domain Name Providers

- https://freedns.afraid.org/
    + Free with some restrictions, should be used for testing
- `<less than 10 digits>.xyz`
    + Less than 1 dollar/year
- https://tld-list.com/
- https://sav.com
    + Cheapest
- https://porkbun.com/products/domains

# DNS utilities / commands

- `dig`, `host`, `nslookup`
    + Basically have similar functionalities, but `dig` has more raw
      data that can be useful in deep dive and debugging. `host` has
      more friendly output.

# References

[wiki-dns]: https://en.wikipedia.org/wiki/Domain_Name_System "Wikipedia - Domain Name System"
[dns-server-types]: https://www.digitalocean.com/community/tutorials/a-comparison-of-dns-server-types-how-to-choose-the-right-dns-configuration "A comparison of DNS Server types: how to choose the right DNS configuration"
[set-up-nameservers]: https://crm.vpscheap.net/knowledgebase.php?action=displayarticle&id=10 "Set up nameservers"
[google-domains-help]: https://support.google.com/domains#topic=3314003 "Google Domains Help"
