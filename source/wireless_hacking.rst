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

Capture packets in the air
==========================

To capture :ref:`packets <cyber501x:unit4_packets_routing>` in the air we use `Airodump-ng <https://www.aircrack-ng.org/doku.php?id=airodump-ng>`_. To see all accessible routers just run command:

.. sourcecode::

    airodump-ng wlp6s0mon
