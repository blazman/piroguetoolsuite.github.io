---
title: "Operate a PiRogue"
date: 2022-05-07
lastmod: 2022-05-07
draft: false
images: []
menu:
  docs:
    parent: "pirogue"
weight: 150
toc: true
resources:
- name: screen
  src: img/screen.png
- name: alerts
  src: img/alerts.png
- name: flows
  src: img/flows.png
- name: world_map
  src: img/world_map.png
- name: general_statistics
  src: img/general_statistics.png
---

## Find your PiRogue on the network
Once your PiRogue is running, it will be accessible to you from the network. There are 2 ways to get the IP address of your PiRogue. 

**The first way** is by looking at the screen of the PiRogue Hat.

{{< img src="screen" alt="The PiRogue's screen" class="d-block mx-auto shadow" >}}

**The second way** is to use the `ping` command. To do so, on your computer connected to the same network as your PiRogue, run the following command:

```bash
ping -c1 pirogue.local
```

Example of output, in this example, the IP address of the PiRogue is `192.168.0.16`:
```text
PING pirogue.local (192.168.0.16) 56(84) bytes of data.
64 bytes from pirogue.home (192.168.0.16): icmp_seq=1 ttl=64 time=0.319 ms

--- pirogue.local ping statistics ---
1 packets transmitted, 1 received, 0% packet loss, time 0ms
rtt min/avg/max/mdev = 0.319/0.319/0.319/0.000 ms
```

## Continuous network traffic analysis

The PiRogue is designed to continuously analyze the network traffic of any device connected to its Wi-Fi network. This means that it is constantly monitoring and inspecting the data packets that are being transmitted and received by these devices. The purpose of this analysis is to identify any suspicious or malicious activity that may be taking place on the network.

### Two-pronged approach to network traffic analysis

The PiRogue employs two primary methods for analyzing network traffic: Deep Packet Inspection (DPI) and [Suricata](https://suricata.io/) rule-based detection.

### Deep Packet Inspection (DPI)

DPI is a technique that allows the PiRogue to examine the contents of data packets in detail. This includes information such as the source and destination IP addresses, the ports being used, the type of data being transmitted, and even the identification of the application involved. By analyzing this information, we can identify patterns and anomalies that may indicate malicious activity.

### Suricata rule-based detection

[Suricata](https://suricata.io/) is an open-source intrusion detection system (IDS) that uses a set of rules to identify known threats. These rules are constantly being updated to keep up with the latest threats. The PiRogue comes pre-configured with rules from [ProofPoint Emerging Threat Open](https://community.emergingthreats.net/t/frequently-asked-questions/56) and [Echap](https://github.com/AssoEchap/stalkerware-indicators), two reputable sources of threat intelligence.

### Visualizing analysis results in the dashboard

The results of the PiRogue's automatic analysis can be visualized in the dashboard. This dashboard provides a graphical overview of the network traffic that has been analyzed, as well as any threats that have been detected. The dashboard also allows users to drill down into the details of specific network flows to learn more about them.


## The dashboard
By default, your PiRogue exposes a [Grafana](https://grafana.com/docs/grafana/latest/basics/) dashboard showing in realtime the ongoing network connections, security alerts and few other information. Checkout the [cheatsheet]({{< relref "cheatsheet" >}}) to get default user and password of the dashboard. 

[Open your dashboard →](http://pirogue.local:3000) 

Depending on your network configuration, this link above may not work. If so, check how to get the IP address of your PiRogue in the previous section.

The default dashboard is composed of different panels, we will go through the main ones.

{{< alert icon="⚠️" context="warning" >}}
The PiRogue keeps 5 days of history, data older than 5 days is automatically deleted. 
{{< /alert >}}

### General statistics
{{< img src="general_statistics" alt="The general statistics panel of the PiRogue's dashboard" class="d-block mx-auto shadow" >}}

This panel displays various information:

1. the number of different devices that have been connected to the PiRogue's Wi-Fi network during the selected period of time
2. the number of security alerts that have occurred during the selected period of time
3. the amount of network traffic exchanged between connected devices and the Internet during the selected period of time
4. the number of network flows that have occurred during the selected period of time
5. the number of different domains that have been contacted during the selected period of time

### World map
{{< img src="world_map" alt="The world map panel of the PiRogue's dashboard" class="d-block mx-auto shadow" >}}

This panel displays the location of the different servers the connected devices have been communicating with during the selected period of time.

### List of flows
{{< img src="flows" alt="The flows panel of the PiRogue's dashboard" class="d-block mx-auto shadow" >}}

This panel displays the different network flows that have occurred during the selected period of time:

1. the time at which the flow as started
2. the category of traffic that has been identified by [NFStream](https://www.nfstream.org/)
3. the type of application that has generating this flow
4. the domain name of the contacted server
5. the IP address of the source of the flow
6. the IP address of the destination of the flow
7. the country where the remote server is located at
8. the amount of network traffic associated to this flow


### List of security alerts
{{< img src="alerts" alt="The alert panel of the PiRogue's dashboard" class="d-block mx-auto shadow" >}}

This panel displays the different security alerts generated by [Suricata](https://suricata.io/) that have occurred during the selected period of time:

1. the time of the alert. If you click on it, you will get the details of the selected alert)
2. the severity of the alert
3. the type of threat associated to the alert
4. the name of the rule corresponding to the alert
5. the IP address of the source of the flow associated to the alert
6. the IP address of the destination of the flow associated to the alert
