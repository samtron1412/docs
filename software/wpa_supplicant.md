[TOC]

# Overview

- [wpa_supplicant][2] is a cross-platform supplicant with support for
  WEP, WPA and WPA2 ([IEEE 802.11i][3]/RSN(Robust Secure Network)).
- wpa_supplicant is the IEEE 802.1X/WPA component that is used in the
  client stations. It implements key negotiation with a WPA
  authenticator and it controls the roaming and IEEE 802.11
  authentication/association of the wireless driver.
- wpa_supplicant is designed to be a "daemon" program that runs in the
  background and acts as the backend component controlling the wireless
  connection.
- wpa_supplicant supports separate frontend programs and a text-based
  frontend (`wpa_cli`) and a GUI (`wpa_gui`) are included.
- wpa_supplicant uses a flexible build configuration that can be used to
  select which features are included.
- Flow
    + wpa_supplicant obtain authentication from a WPA authenticator. It
      must be configured to do that.
    + Once the authentication is successful, obtaining an IP by setting
      it manually with the `iproute2` suite or using some networking
      program, like `systemd-network` or `dhcpcd`, to configure an
      interface to obtain an IP address automatically via DHCP.

# Connecting with wpa_cli

- wpa_cli allows
    + scanning for the available networks
    + interactively configure wpa_supplicant at runtime
- wpa_supplicant must be given the rights to update the configuration.
  Creating a minimal configuration file:
    + `update_config=1`: allows wpa_supplicant to overwrite
      configuration file whenever configuration is changed.
    + `ctrl_interface=/var/run/wpa_supplicant`: is a UNIX domain socket.
      wpa_supplicant will listen requests from external programs
      (CLI/GUI) through this socket.
    + `ctrl_interface_group=wheel`: allows only members of the wheel
      group to use the socket.

```
/etc/wpa_supplicant/example.conf

ctrl_interface=/var/run/wpa_supplicant
ctrl_interface_group=wheel
update_config=1
```

- Starting wpa_supplicant with:
    + Using `ip link` command to discover the wireless network interface
      name, and using the command: `# wpa_supplicant -B -i interface -c
      /etc/wpa_supplicant/example.conf`
    + If the wpa_supplicant is already running at boot then we don't
      need to start wpa_supplicant manually. Go to the next step.

- `$ wpa_cli`
    + Use the `scan` and `scan_results` commands to see the available
    networks:

        ```
        > scan
        OK
        <3>CTRL-EVENT-SCAN-RESULTS
        > scan_results
        bssid / frequency / signal level / flags / ssid
        00:00:00:00:00:00 2462 -49 [WPA2-PSK-CCMP][ESS] MYSSID
        11:11:11:11:11:11 2437 -64 [WPA2-PSK-CCMP][ESS] ANOTHERSSID
        ```

    + To associate with `MYSSID`, add the network, set the credentials
    and enable it:

        ```
        > add_network
        0
        > set_network 0 ssid "MYSSID"
        > set_network 0 psk "passphrase"
        > enable_network 0
        <2>CTRL-EVENT-CONNECTED - Connection to 00:00:00:00:00:00 completed (reauth) [id=0 id_str=]
        ```

        * Get the hash of passphrase through `wpa_passphrase ssid
        passphrase`
    + Finally save this network in the configuration file: `save_config`

# Connecting with wpa_passphrase

# Configuration

# Connection

# Tips and Tricks

## Saving passphrase as a hash (encrypted passphrase) - WPA2-Enterprise - EAP (PEAP) - MSCHAPv2

- Using md4 hash

# Troubleshooting

# References

[1]: https://wiki.archlinux.org/index.php/WPA_supplicant "Arch Wiki - WPA supplicant"
[2]: http://w1.fi/wpa_supplicant/ "Homepage"
[3]: https://en.wikipedia.org/wiki/IEEE_802.11i "Wikipedia - IEEE 802.11i"
