[TOC]

# About
## Tor Overview
### Inception
Tor was originally designed, implemented, and deployed as a third-generation [onion routing project of the U.S. Naval Research Laboratory](http://www.onion-router.net/). It was originally developed with the U.S. Navy in mind, for the primary purpose of protecting government communications. Today, it is used every day for a wide variety of purposes by **normal people, the military, journalists, law enforcement officers, activists, and many others**.

### Overview
Tor is a network of *virtual tunnels* that allows people and groups to improve their privacy and security on the Internet. It also enables software developers to create new communication tools with built-in privacy features.

**Individuals** use Tor to keep websites from tracking them and their family members, or to connect to news sites, instant messaging services, or the like when these are blocked by their local Internet providers. Individuals also use Tor for socially *sensitive communication*: chat rooms and web forums for rape and abuse survivors, or people with illnesses. [Tor's hidden services](https://www.torproject.org/docs/hidden-services.html.en) let users publish web sites and other services without needing to reveal the location of the site.

**Journalists** use Tor to communicate more safely with *whistleblowers* and *dissidents*. Non-governmental organizations (NGOs) use Tor to allow their workers to connect to their home website while they're in a foreign country, without notifying everybody nearby that they're working with that organization.

**Groups** such as Indymedia recommend Tor for safeguarding their members' online privacy and security. **Activist** groups like the Electronic Frontier Foundation (EFF) recommend Tor as a mechanism for maintaining civil liberties online. **Corporations** use Tor as a safe way to conduct competitive analysis, and to protect sensitive procurement patterns from eavesdroppers.

**A branch of the U.S. Navy** uses Tor for open source intelligence gathering, and one of its teams used Tor while deployed in the Middle East recently. **Law enforcement** uses Tor for visiting or surveilling web sites without leaving government IP addresses in their web logs, and for security during sting operations.

### Why we need Tor
Using Tor protects you against a common form of **Internet surveillance** known as "**traffic analysis**." Traffic analysis can be used to infer who is talking to whom over a public network. Knowing the source and destination of your Internet traffic allows others to track your *behavior* and *interests*.

**How does traffic analysis work?** Internet data packets have two parts: a *data payload* and a *header* used for routing. The data payload is whatever is being sent, whether that's an email message, a web page, or an audio file. Even if you encrypt the data payload of your communications, traffic analysis still reveals a great deal about what you're doing and, possibly, what you're saying. That's because it focuses on the header, which discloses source, destination, size, timing, and so on.

A very simple form of traffic analysis might involve sitting somewhere between sender and recipient on the network, looking at headers. But there are also more powerful kinds of traffic analysis. Some **attackers** spy on multiple parts of the Internet and use sophisticated statistical techniques to track the communications patterns of many different organizations and individuals. Encryption does not help against these attackers, since it only hides the content of Internet traffic, not the headers.

### The solution: a distributed, anonymous network
![]

Tor helps to reduce the risks of both simple and sophisticated traffic analysis by distributing your transactions over several places on the Internet, so no single point can link you to your destination. Instead of taking a direct route from source to destination, data packets on the Tor network take **a random pathway through several relays** that cover your tracks so no observer at any single point can tell where the data came from or where it's going.

To create a private network pathway with Tor, the user's software or client incrementally builds **a circuit of encrypted connections through relays** on the network. The circuit is extended one hop at a time, and *each relay along the way knows only which relay gave it data and which relay it is giving data to*. No individual relay ever knows the complete path that a data packet has taken. *The client negotiates a separate set of encryption keys for each hop along the circuit* to ensure that each hop can't trace these connections as they pass through.

<figure>
  <figcaption style="text-align:center;">How Tor Work 2</figcaption>
  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
  <img src="tor_figures/htw2.png" alt="How Tor Work 2" title="How Tor Work 2">
</figure>

Tor only works for TCP streams and can be used by any application with SOCKS support.

For efficiency, the Tor software *uses the same circuit for connections that happen within the same ten minutes* or so. Later requests are given a new circuit, to keep people from linking your earlier actions to the new ones.

<figure>
  <figcaption style="text-align:center;">How Tor Work 3</figcaption>
  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
  <img src="tor_figures/htw3.png" alt="How Tor Work 3" title="How Tor Work 3">
</figure>

### Hidden services
Tor also makes it possible for users to hide their locations while offering various kinds of services, such as **web publishing** or **an instant messaging server**. Using Tor "rendezvous points," other Tor users can connect to these hidden services, each without knowing the other's network identity. This hidden service functionality could allow Tor users to set up a website where people publish material without worrying about *censorship*. Nobody would be able to determine who was offering the site, and nobody who offered the site would know who was posting to it. Learn more about [configuring hidden services](https://www.torproject.org/docs/tor-hidden-service.html.en) and how the [hidden service protocol](https://www.torproject.org/docs/hidden-services.html.en) works.

### Staying anonymous
Tor can't solve all anonymity problems. It focuses only on protecting the transport of data. You need to use protocol-specific support software if you don't want the sites you visit to see your identifying information.

### The future of Tor
Providing a usable anonymizing network on the Internet today is an ongoing challenge. Please consider [running a relay](https://www.torproject.org/docs/tor-doc-relay.html.en) or [volunteering](https://www.torproject.org/getinvolved/volunteer.html.en) as a [developer](https://www.torproject.org/docs/documentation.html.en#Developers).

# [Documentation](https://www.torproject.org/docs/documentation.html.en)
## Want Tor to really work?
You need to change some of your habits, as some things won't work exactly as you are used to.

### Use the Tor Browser
Tor does not protect all of your computer's Internet traffic when you run it. Tor only protects your applications that are properly configured to send their Internet traffic through Tor. To avoid problems with Tor configuration, we strongly recommend you use the Tor Browser Bundle. It is pre-configured to protect your privacy and anonymity on the web as long as you're browsing with the Tor Browser itself. Almost any other web browser configuration is likely to be unsafe to use with Tor.

### Don't torrent over Tor
Torrent file-sharing applications have been observed to ignore proxy settings and make direct connections even when they are told to use Tor. Even if your torrent application connects only through Tor, you will often send out your real IP address in the tracker GET request, because that's how torrents work. Not only do you deanonymize your torrent traffic and your other simultaneous Tor web traffic this way, you also slow down the entire Tor network for everyone else.

### Don't enable or install browser plugins
The Tor Browser will block browser plugins such as Flash, RealPlayer, Quicktime, and others: they can be manipulated into revealing your IP address. Similarly, we do not recommend installing additional addons or plugins into the Tor Browser, as these may bypass Tor or otherwise harm your anonymity and privacy. The lack of plugins means that Youtube videos are blocked by default, but Youtube does provide an experimental opt-in feature (enable it here) that works for some videos.

### Use HTTPS versions of websites
Tor will encrypt your traffic to and within the Tor network, but the encryption of your traffic to the final destination website depends upon on that website. To help ensure private encryption to websites, the Tor Browser Bundle includes HTTPS Everywhere to force the use of HTTPS encryption with major websites that support it. However, you should still watch the browser URL bar to ensure that websites you provide sensitive information to display a blue or green URL bar button, include https:// in the URL, and display the proper expected name for the website. Also see EFF's interactive page explaining how Tor and HTTPS relate.

### Don't open documents downloaded through Tor while online
The Tor Browser will warn you before automatically opening documents that are handled by external applications. DO NOT IGNORE THIS WARNING. You should be very careful when downloading documents via Tor (especially DOC and PDF files) as these documents can contain Internet resources that will be downloaded outside of Tor by the application that opens them. This will reveal your non-Tor IP address. If you must work with DOC and/or PDF files, we strongly recommend either using a disconnected computer, downloading the free VirtualBox and using it with a virtual machine image with networking disabled, or using Tails. Under no circumstances is it safe to use BitTorrent and Tor together, however.

### Use bridges and/or find company
Tor tries to prevent attackers from learning what destination websites you connect to. However, by default, it does not prevent somebody watching your Internet traffic from learning that you're using Tor. If this matters to you, you can reduce this risk by configuring Tor to use a Tor bridge relay rather than connecting directly to the public Tor network. Ultimately the best protection is a social approach: the more Tor users there are near you and the more diverse their interests, the less dangerous it will be that you are one of them. Convince other people to use Tor, too!

## Documentation Overview

## [Installation](https://www.torproject.org/docs/tor-doc-windows.html.en)
[Torify HOWTO](https://trac.torproject.org/projects/tor/wiki/doc/TorifyHOWTO)

## Manuals

## Wiki

## General FAQ

## Abuse FAQ

## Trademark FAQ

## Legal FAQ

## DMCA Response
