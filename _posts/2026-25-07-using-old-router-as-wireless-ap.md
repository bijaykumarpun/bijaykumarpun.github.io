---
layout: post
title: "Huawei ONT Access Point Setup"
date: 2026-07-25 08:00:00
description: "Turning a Huawei Router into a Wireless Access Point (LAN to LAN)"
---
# 

## Summary

When repurposing an old Huawei router as a secondary router connected via a LAN cable, simply plugging the secondary router into the primary router wasn't enough. The device required a few configuration changes before it could function as a wireless access point (AP).

The steps below show how to configure a **Huawei EchoLife EG8141A5** as a wireless access point using a **LAN-to-LAN connection**.

> **Note:** Some settings and menus may vary depending upon router model

---

## Steps

### 1. Connect the Routers

Use an Ethernet (LAN) cable to connect the primary router to the secondary router.

- Connect one end of the cable to a LAN port on the primary router.
- Connect the other end to a LAN port on the secondary router.

> Do not use WAN port on the secondary router when configuring it as an access point.

---

### 2. Log in to the Secondary Router

For the **Huawei EchoLife EG8141A5**, log in using the **super admin** account, which provides access to additional settings that are not available to regular users.

```text
Username: Epadmin
Password: adminEp
```

> *Credentials may vary

---

### 3. Enable LAN Port Configuration

> Some routers have LAN ports enabled by default, so this step may not be necessary.

Navigate to:

```text
Advanced → LAN → Layer 2/3 Port
```

- Check the box for the LAN port being used for the connection.
- Click **Apply**.

---

### 4. Change the Router's IP Address

The secondary router should be assigned an IP address that belongs to the same subnet as the primary router.

For example:

| Device | IP Address |
|-------|------------|
| Primary Router | `192.168.18.1` |
| Secondary Router | `192.168.18.2` |

Navigate to:

```text
Advanced → LAN → LAN Host
```

Under **Primary Address**, enter a new IP address that:

- Is within the same subnet as the primary router.
- Is not already in use by another device.

If a **Secondary Address** option is available, it can be disabled.

Click **Apply** when finished.

> A subnet is simply the shared network portion of an IP address. If primary router uses `192.168.18.x`, the secondary router should also use `192.168.18.x`.

---

### 5. Disable the DHCP Server

The DHCP server should be disabled on the secondary router so that only the primary router assigns IP addresses to devices on the network.

> **DHCP** = **Dynamic Host Configuration Protocol**.

Having multiple DHCP servers on the same network can lead to IP conflicts and connectivity issues.

Navigate to:

```text
Advanced → LAN → DHCP Server
```

- Uncheck **Enable Primary DHCP Server**.
- Click **Apply**.

---

## Done!

After completing the above steps, the secondary Huawei router should function as a **wireless access point**, thereby extending the existing Wi-Fi network while relying on the primary router for network management.

A reboot may or may not be required, depending on the router model.

```
Final topology:
  Internet → Primary Router (192.168.18.1)
            └── LAN Cable
                  └── Secondary Router (192.168.18.2)
                        └── Wireless Clients
```



----

##### TEXTDUMP
```
##### terminal history
 428  route -n get default | grep gateway
  429  route -n get default
  430  route
  431  netstat
  432  netstat -nr | grep default
  433  networksetup -getinfo wi-fi
  434  netstat -nr | grep default
  435  route -n get default
  436  route -n get default | grep gateway
  437  ipconfig getifaddr en0
  438  ipconfig getifaddr en0
  439  ipconfig getifaddr en0
  440  ipconfig getifaddr en0
  441  ipconfig getifaddr en0
  ```

```
##### Search history
echolife eg8141a5 admin login
reddit setup huawei echolife eg8141a5 as AP
````

```
##### ChatGPT Log
Connected Huawei EchoLife EG8141A5 to primary router using LAN cable.
Verified physical link LEDs on both routers.
Attempted LAN-to-LAN connection without additional configuration.
Secondary router Wi-Fi was visible but no internet access.
Confirmed WAN port was not in use.
Logged into router using default admin account.
Insufficient permissions detected.
Logged into router using Epadmin credentials.
Navigated to Advanced settings.
Discovered Layer 2/3 Port configuration menu.
Enabled required LAN port.
Applied LAN port changes.
Verified primary router IP address.
Primary router IP: 192.168.18.1
Navigated to LAN Host settings.
Current secondary router IP: 192.168.100.1
Updated secondary router IP to 192.168.18.2
Disabled Secondary Address.
Applied IP address changes.
Reconnected to router using updated IP address.
Verified router accessibility at 192.168.18.2
Navigated to DHCP Server settings.
Detected Primary DHCP Server enabled.
Disabled Primary DHCP Server.
Applied DHCP configuration changes.
Verified DHCP server state: Disabled.
Restarted secondary router.
Established LAN-to-LAN connection.
Verified wireless SSID broadcast.
Connected test device to secondary router Wi-Fi.
Requested IP address from network.
Received IP address from primary router.
Assigned IP: 192.168.18.15
Verified subnet mask.
Verified default gateway.
Gateway: 192.168.18.1
Performed internet connectivity test.
Internet access confirmed.
Verified access to primary router admin panel.
Verified access to secondary router admin panel.
Confirmed both routers are within same subnet.
Confirmed no IP conflicts detected.
Confirmed no double NAT.
Confirmed NAT handled by primary router.
Confirmed DHCP handled by primary router.
Confirmed wireless access point functionality.
Observed seamless connectivity across access points.
No factory reset required.
No additional firmware changes required.
Configuration completed successfully.
Final topology established.
Internet → Primary Router → Secondary Router (AP) → Wireless Clients
```


