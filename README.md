# Secure-the-Network 

## Project Overview

This project was created for my **Network Security module**.

The aim of the project was to take a pre-built network in Cisco Packet Tracer and add different network security technologies and features to make the network more secure.

The project included several areas of network security, including:

- Network device hardening
- Secure remote access using SSH
- AAA authentication
- Site-to-site IPsec VPN
- OSPF routing security
- Access Control Lists (ACLs)
- Firewall rules
- Layer 2 switch security
- DHCP snooping
- NTP and Syslog monitoring
- Network Address Translation (PAT)

The project also required me to document the work in a report and complete an in-person demonstration showing the security features working.

---

## Network Overview

The network contains three main sites:

- **Dublin**
- **London**
- **Beijing**

Dublin contains separate **Sales and Purchasing VLANs**.

London contains the **server network and Admin network**.

Beijing represents a remote site that connects to the rest of the network using a **site-to-site VPN**.

The network was built and configured using **Cisco Packet Tracer**.

---

## Security Features

The project includes several different security controls.

### Network Device Hardening

The routers and switches were hardened to reduce the risk of unauthorised access.

I configured:

- Secure passwords
- Console security
- VTY line security
- SSH version 2
- Login timeouts
- Local authentication
- Restricted remote management

I also disabled or secured unused switch ports where possible.

---

### Secure Remote Access

SSH was used instead of Telnet for remote management.

SSH version 2 was enabled on the network devices so that administrator login details and management traffic were encrypted.

AAA was also configured using the London RADIUS server.

This allowed administrator accounts to be managed centrally rather than creating separate accounts on every device.

A local administrator account was also kept as a backup in case the AAA server became unavailable.

---

### Site-to-Site VPN

A site-to-site IPsec VPN was configured between the **Dublin and Beijing routers**.

The VPN protects traffic travelling between the two sites.

The VPN used:

- AES encryption for the IKE policy
- SHA authentication
- Pre-shared key authentication
- Diffie-Hellman group 2
- IPsec transform sets
- Crypto maps
- ACLs to identify the traffic that should use the VPN

The VPN was tested by sending traffic between the Dublin and Beijing networks.

---

### Routing Security

OSPF was used between the Dublin and London routers.

Message-digest authentication was added to the OSPF connection.

This means that the routers need matching authentication information before they can exchange routing information.

The OSPF neighbour relationship was tested to make sure it reached the **FULL** state after the security settings were added.

---

### Firewall and Access Control Lists

Extended ACLs were used to control traffic between different parts of the network.

For example, the Sales and Purchasing networks were separated so that they could not directly communicate with each other.

The ACLs still allowed normal traffic such as access to the correct gateway and required services.

Beijing was also restricted so that it could access the services and networks it needed without having unrestricted access to the internal network.

This was based on the idea of **least privilege**, where users and devices should only have the access they actually need.

---

### Layer 2 Switch Security

Security was also added to the switches.

Port security was configured on endpoint ports using sticky MAC addresses.

The ports were configured to allow a limited number of MAC addresses and restrict unauthorised devices.

PortFast and BPDU Guard were also used on suitable endpoint ports.

Unused ports were moved into a separate unused VLAN and shut down.

This helps reduce the risk of someone connecting an unauthorised device to an unused switch port.

---

### DHCP Snooping

DHCP snooping was configured on the Dublin switches.

This helps protect the network from rogue DHCP servers.

The correct DHCP server and required uplinks were trusted, while normal client ports were left untrusted.

This means that a normal endpoint cannot pretend to be a DHCP server and provide incorrect network settings to other devices.

---

### NTP and Syslog Monitoring

NTP and Syslog were configured to improve network monitoring.

The NTP server was located on the London server network.

NTP keeps the clocks on the network devices synchronised.

This is useful when investigating security incidents because logs from different devices can be compared using accurate timestamps.

Syslog was also configured so that routers and switches could send their log messages to a central Syslog server.

This gives the administrator one place to check network events instead of having to check every device individually.

---

### PAT

PAT was configured on the London router.

This allows devices using private IP addresses on the London Admin network to share the public IP address of the router.

For example, an internal address such as:

```text
192.168.4.x
