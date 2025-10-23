# NSDSS_Hackathon

# 🚀 Solar System Network Challenge 🚀

Welcome to our Packet Tracer Hackathon Project! This repository contains a Cisco Packet Tracer `.pkt` file with a complex, space-themed network topology. Your mission is to solve a series of 8 networking challenges to get the entire solar system communicating efficiently and securely.

This project was created in collaboration with:
* [https://github.com/RORO123b](https://github.com/RORO123b)
* [https://github.com/MargaritAndrei](https://github.com/MargaritAndrei)

---

## The Challenges

The project is divided into 8 main tasks. Follow them in order to build the network from the ground up.

### Task 1: Device Hostnames

Your first task is to set the hostnames for all major devices in the topology according to the provided list. This helps in identifying routers and switches during configuration.

**Devices to name:**
`Soare`, `RouterPamant`, `Luna`, `Asia`, `China`, `CoreeaDeNord`, `Europa`, `Romania`, `Germania`, `RouterJupiter`, `Io`, `Ganymede`, `Callisto`, `AlienSpaceship`, `RouterSaturn`, `LaVacaSaturnaSaturnita`, `Satelit`

---

### Task 2: VLSM Address Planning

Before configuring interfaces, you must plan the IP addressing scheme. You've been given the main network block **`175.234.0.0/16`**.

Your task is to subnet this block to create the following networks:
* **`asia` network:** Requires space for at least 254 hosts.
    * *Solution Network:* `175.234.0.0/24`
* **`europa` network:** Requires space for at least 126 hosts.
    * *Solution Network:* `175.234.1.0/25`
* **`luna` network:** Requires space for at least 6 hosts.
    * *Solution Network:* `175.234.1.128/29`

---

### Task 3: IP Address Configuration

With the plan from Task 2, your next step is to configure the interfaces and end devices.

1.  **Configure `RouterPamant`:** Assign the correct IP addresses to its GigabitEthernet interfaces (`0/0`, `0/1`, `0/2`) to act as the default gateway for the `luna`, `europa`, and `asia` networks, respectively.
2.  **Configure End Devices:** Manually assign the static IP address, subnet mask, and default gateway for all PCs and servers in the `asia`, `europa`, and `luna` networks.
3.  **Configure Alien Network:** Separately, configure the devices in the `102.102.102.0/24` network (e.g., `Astronaut_0`, `Alien_2`, `Alien_3`) with their static IPs.

---

### Task 4: VLAN Configuration

Move to the `Satelit` switch. Your task is to segment the network using VLANs.

1.  Create **VLAN 10**, **VLAN 20**, and **VLAN 30**.
2.  Configure interface `Fa0/1` as a **trunk port** to carry traffic for all VLANs.
3.  Assign interfaces `Fa0/2`, `Fa0/3`, and `Fa0/4` as **access ports** for VLANs 10, 20, and 30, respectively.

---

### Task 5: Inter-VLAN Routing (Router-on-a-Stick)

The devices on different VLANs on the `Satelit` switch can't communicate yet. Your task is to enable routing between them.

On the `LaVacaSaturnaSaturnita` router:
1.  Configure **sub-interfaces** on `GigabitEthernet0/1` for each VLAN (e.g., `g0/1.10`, `g0/1.20`, `g0/1.30`).
2.  Set the encapsulation to **`dot1q`** for each sub-interface, tagging it with the correct VLAN ID.
3.  Assign the correct gateway IP addresses for each VLAN (VLAN 10: `69.69.69.1/24`, VLAN 20: `100.100.100.1/24`, VLAN 30: `200.200.200.1/24`).
4.  Activate the physical `Gig0/1` interface.

---

### Task 6: EtherChannel (LACP)

To increase bandwidth and provide redundancy between the `Callisto` and `AlienSpaceship` switches, you will configure an EtherChannel.

1.  On both switches, bundle the specified FastEthernet interfaces into **Port-Channel 1**.
2.  Configure the channel-group to use **LACP** (Link Aggregation Control Protocol) by setting the mode to `active`.
3.  Configure the resulting logical `Port-Channel 1` interface as an `access` port.

---

### Task 7: OSPF Dynamic Routing

The core routers of the solar system (`Soare`, `Pamant`, `RouterJupiter`, `RouterSaturn`) need to share routing information automatically.

Your task is to configure **single-area OSPF (Area 0)** on all four routers:
1.  Enable `router ospf 1` on all core routers.
2.  Assign a unique **router-ID** to each (`5.5.5.5` for Soare, `7.7.7.7` for Pamant, etc.).
3.  Advertise the directly connected networks involved in the core routing (e.g., `10.0.0.0`, `20.0.0.0`, `30.0.0.0`, `40.0.0.0`).
4.  **Important:** Modify the OSPF timers on the serial interfaces, setting the **hello-interval to 15** seconds and the **dead-interval to 25** seconds.

---

### Task 8: Access Control List (ACL)

Finally, you must implement a security policy. The aliens (`Alien_2` and `Alien_3`) are not allowed to host web services.

1.  On `RouterJupiter`, create an **extended numbered ACL (110)**.
2.  This ACL must **deny** any traffic destined for `Alien_2` (`102.102.102.4`) on ports **80 (HTTP)** and **443 (HTTPS)**.
3.  Add identical rules to **deny** web access to `Alien_3` (`102.102.102.5`).
4.  Remember to **permit all other IP traffic** at the end of the ACL.
5.  Apply this ACL to the `GigabitEthernet0/1` interface in the **outbound** direction.

---

Good luck, and have fun!
