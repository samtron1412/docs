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
    * DNS Records
        - DNS record is an object in a hosted zone that you use to define
          how you want to route traffic for the domain or a subdomain.
        - SOA (Start of Authority) records: are configured by the
          DNS service provider automatically, so we don't need to
          configure these.
        - DNS zone records:
            + Domain
            + Time to live
            + Class
            + Type
                * https://en.wikipedia.org/wiki/List_of_DNS_record_types
                * A: tie the domain or subdomain to an IPv4 address
                * AAAA: tie the domain or subdomain to an IPv6 address.
                * CNAME: tie the domain or subdomain to another domain or subdomain
                * MX: define how mail is handled for your domain,
                  including: priority (lower number is higher
                  priority) and answering mail server domain name.
                * TXT: associate text data with your domain. Is used
                  for SPF or DKIM.
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
