[TOC]

# Overview
- [wpa_supplicant][2] is a cross-platform supplicant with support for WEP, WPA and WPA2 ([IEEE 802.11i][3]/RSN(Robust Secure Network)).
- wpa_supplicant is the IEEE 802.1X/WPA component that is used in the client stations. It implements key negotiation with a WPA authenticator and it controls the roaming and IEEE 802.11 authentication/association of the wireless driver.
- wpa_supplicant is designed to be a "daemon" program that runs in the background and acts as the backend component controlling the wireless connection.
- wpa_supplicant supports separate frontend programs and a text-based frontend (`wpa_cli`) and a GUI (`wpa_gui`) are included.
- wpa_supplicant uses a flexible build configuration that can be used to select which features are included.
- Flow
	+ wpa_supplicant obtain authentication from a WPA authenticator. It must be configured to do that.
	+ Once the authentication is successful, obtaining an IP by setting it manually with the `iproute2` suite or using some networking program, like `systemd-network` or `dhcpcd`, to configure an interface to obtain an IP address automatically via DHCP.

# Saving passphrase as a hash (encrypted passphrase)
- Using wpa_passphrase
- Using md4 haskh

# References
[1]: https://wiki.archlinux.org/index.php/WPA_supplicant "Arch Wiki - WPA supplicant"
[2]: http://w1.fi/wpa_supplicant/ "Homepage"
[3]: https://en.wikipedia.org/wiki/IEEE_802.11i "Wikipedia - IEEE 802.11i"
