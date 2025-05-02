

## Summary of Routing Concepts (Chapters 1-3)

### Chapter 1: Routing Concepts

This chapter introduces the fundamental concepts of routers and routing.

**1.1 Initial Router Configuration**

- **Router Functions & Characteristics:**
    - Routers are responsible for routing traffic between different networks.
    - Key network characteristics include topology, speed, cost, security, availability, scalability, and reliability.
    - Routers are specialized computers containing a CPU, OS (like Cisco IOS), RAM, ROM, NVRAM, and Flash memory.
        - **RAM:** Stores running IOS, running configuration file, IP routing and ARP tables, packet buffer.
        - **ROM:** Stores bootup instructions, basic diagnostic software, limited IOS.
        - **NVRAM:** Stores the startup configuration file.
        - **Flash:** Stores the IOS and other system files.
    - Routers use specialized network interfaces and ports to connect networks.
- **Connecting Devices:**
    - Devices need an IP address, subnet mask, and default gateway to access network resources.
    - The default gateway is the router interface IP address used to send packets when the destination is not on the local network.
    - IP addressing can be static (manually assigned) or dynamic (assigned by DHCP). Static IPs are often used for servers, printers, and small networks. Most hosts use DHCP.
    - Network documentation should include device names, interfaces, IP addresses, subnet masks, and default gateways.
    - Switches also need IP addresses for remote management, assigned to a Switched Virtual Interface (SVI).
- **Basic Router Settings:**
    - Assign a unique hostname.
    - Secure management access (privileged EXEC, user EXEC, Telnet) and encrypt passwords.
    - Configure a login banner for legal notices.
    - Save the configuration.
- **Interface Configuration (IPv4 & IPv6):**
    - Interfaces need an IP address and subnet mask.
    - Must be activated using the `no shutdown` command.
    - Serial interfaces require clock rate configuration on the DCE side.
    - IPv6 interfaces are configured using `ipv6 address <ipv6-address>/<prefix-length>` [e.g., global unicast, EUI-64, link-local] and activated with `no shutdown`.
    - Loopback interfaces are logical, always 'up', useful for testing and OSPF.
- **Verification:**
    - Use commands like `show ip interface brief`, `show ip route`, `show running-config`, `show interfaces`, `show ip interfaces` to verify IPv4 interface settings.
    - Use `show ipv6 interface brief`, `show ipv6 interface <interface>`, `show ipv6 route` for IPv6 verification.
    - Filter command output using `|` followed by `section`, `include`, `exclude`, or `begin`.
    - Use the command history feature (Ctrl+P/Up Arrow, Ctrl+N/Down Arrow, `show history`).

**1.2 Routing Decisions**

- **Packet Switching:** Routers switch packets between interfaces by de-encapsulating and re-encapsulating them as they move from one network type to another.
- **Path Determination:** Routers use their routing table to determine the best path to forward a packet.
    - **Best Path Selection:** Based on metrics (the value used to measure distance). The path with the lowest metric is best.
        - **RIP Metric:** Hop count.
        - **OSPF Metric:** Cost (based on cumulative bandwidth).
        - **EIGRP Metric:** Bandwidth, delay, load, reliability.
    - **Load Balancing:** If multiple paths to a destination have equal cost metrics, the router distributes packets across these paths equally. This can be configured for dynamic protocols and static routes.
    - **Administrative Distance (AD):** Used when multiple routing sources provide a route to the same destination. The route with the lowest AD is preferred and installed in the routing table.
        - Directly Connected: AD 0.
        - Static Route: AD 1.
        - EIGRP: AD 90.

**1.3 Router Operation**

- **Routing Table:** Stored in RAM, contains information about directly connected and remote routes.
- **Routing Table Sources:**
    - **Directly Connected Networks:** Added when an interface is configured with an IP address and is active ('up'). Have an AD of 0. Identified by 'C' and 'L' (Local interface route, IOS 15+) in `show ip route` output.
    - **Static Routes:** Manually configured by an administrator. Define an explicit path. Must be updated manually if topology changes. AD of 1.
    - **Dynamic Routing Protocols (e.g., EIGRP, OSPF):** Automatically learn about remote networks from other routers. They discover networks and maintain routing tables dynamically. Routers converge when they all have consistent routing information. Each protocol has its own AD (e.g., EIGRP=90, OSPF=110).

### Chapter 2: Static Routing

This chapter focuses on the configuration and implementation of static routes.

**2.1 Implementing Static Routing**

- **Learning Remote Routes:** Routers learn remote networks either manually (static routes) or dynamically (dynamic routing protocols).
- **Why Use Static Routing?**
    - Improved security (routes aren't advertised).
    - Less bandwidth and CPU usage compared to dynamic protocols.
    - Path predictability.
- **When to Use Static Routes:**
    - Small networks where routing table maintenance is easy.
    - Routing to and from stub networks (networks accessible via a single route).
    - Using a single default route as a gateway of last resort.
    - Connecting to a specific network.
    - Summarizing multiple contiguous networks into one static route.
    - Creating a backup route (floating static route).
- **Types of Static Routes:**
    - **Standard Static Route:** Manually defined route to a specific remote network.
    - **Default Static Route:** Matches all packets that don't have a more specific match in the routing table. Uses `0.0.0.0/0` (IPv4) or `::/0` (IPv6) as the destination. Acts as a gateway of last resort.
    - **Summary Static Route:** Aggregates multiple specific routes into a single, less specific route.
    - **Floating Static Route:** A static route with a higher Administrative Distance than another route (static or dynamic). It acts as a backup, only used if the primary route fails.

**2.2 Configuring Static and Default Routes**

- **IPv4 Static Route Command:** `ip route <network-address> <subnet-mask> { <next-hop-ip> | <exit-interface> }`.
- **Next-Hop Options:**
    - **Next-Hop Route:** Specifies only the next-hop IP address.
    - **Directly Connected Static Route:** Specifies only the router's exit interface. Recommended for point-to-point serial links.
    - **Fully Specified Static Route:** Specifies both the next-hop IP and the exit interface. Recommended for multi-access interfaces like Ethernet.
- **IPv4 Default Route Command:** `ip route 0.0.0.0 0.0.0.0 { <next-hop-ip> | <exit-interface> }`.
- **IPv6 Static Route Command:** `ipv6 route <ipv6-prefix>/<prefix-length> { <next-hop-ipv6> | <exit-interface> }`. Next-hop options are similar to IPv4. Often, the next-hop IPv6 address will be the link-local address of the neighboring router.
- **IPv6 Default Route Command:** `ipv6 route ::/0 { <next-hop-ipv6> | <exit-interface> }`.
- **Floating Static Route Configuration:** Configure a static route as usual, but add an administrative distance value at the end of the command (higher than the primary route's AD). Example: `ip route 0.0.0.0 0.0.0.0 Serial0/0/1 5` (AD of 5).
- **Host Routes:** Routes to a specific host IP address.
    - Automatically installed for the router's own interface addresses (marked with 'L' in the routing table).
    - Can be configured statically using a /32 mask (IPv4) or /128 mask (IPv6). Example: `ip route 192.168.5.1 255.255.255.255 <next-hop/exit-intf>`.
- **Verification:** Use `show ip route`, `show ipv6 route`, `ping`, `traceroute`. Use `show ip route static` or `show ipv6 route static` to see only static routes.

**2.3 Troubleshooting Static and Default Routes**

- **Packet Processing:** When a packet arrives, the router looks for the most specific match in the routing table (longest prefix match). If a static route is the best match, the packet is forwarded according to that route. If no match exists (and no default route), the packet is dropped.
- **Common Issues:** Missing or misconfigured static/default routes are common problems.
- **Troubleshooting Steps:**
    1. Use `ping` to test connectivity to the destination. Extended ping can specify the source IP.
    2. Use `traceroute` to identify the hop where connectivity fails. An ICMP "Destination Unreachable" message might be received.
    3. Use `show ip route` or `show ipv6 route` to examine the routing table for missing or incorrect entries.
    4. Use `show ip interface brief` or `show ipv6 interface brief` to check interface status.
    5. Use `show cdp neighbors detail` (if Cisco devices) to verify Layer 1/Layer 2 connectivity.

### Chapter 3: Dynamic Routing

This chapter introduces dynamic routing protocols and contrasts them with static routing.

**3.1 Dynamic Routing Protocols**

- **Purpose:** Used by routers to automatically share information about remote network reachability and status.
- **Functions:**
    - Discover remote networks.
    - Maintain up-to-date routing information.
    - Choose the best path to destinations.
    - Find a new best path if the current path becomes unavailable.
- **Components:**
    - **Data Structures:** Typically tables or databases stored in RAM (e.g., neighbor table, topology table).
    - **Routing Protocol Messages:** Used to discover neighbors, exchange routing info, etc..
    - **Algorithm:** Used for processing routing information and best path determination.
- **Dynamic vs. Static:** Networks often use a combination.
    - **Static Use Cases:** Small/stable networks, stub networks, default routes.
    - **Static Advantages:** Security, less overhead (bandwidth/CPU), predictable path.
    - **Static Disadvantages:** Manual configuration/updates, error-prone, not scalable.
    - **Dynamic Advantages:** Automatic network discovery/updates, less admin overhead, scalable.
    - **Dynamic Disadvantages:** Requires CPU/memory/bandwidth, can be complex, less secure initially.

**3.2 RIPv2 (Example Dynamic Protocol)**

- **Configuration Mode:** `router rip` enters RIP configuration mode.
- **Enable RIPv2:** Use the `version 2` command.
- **Advertise Networks:** Use the `network <classful-network-address>` command. RIPv2 sends updates for subnets within this classful boundary.
- **Disable Auto-Summary:** Use `no auto-summary`. This prevents RIPv2 from summarizing networks to their classful boundaries at network borders, allowing for discontiguous networks and VLSM. Use `show ip protocols` to verify.
- **Passive Interfaces:** Use `passive-interface <interface-name>` or `passive-interface default` to prevent RIP updates from being sent out specific interfaces (like LAN interfaces). This saves bandwidth/resources and improves security.
- **Default Route Propagation:** A router with a default route (e.g., `ip route 0.0.0.0 0.0.0.0 <next-hop/exit-intf>`) can advertise it to other RIP routers using the `default-information originate` command.
- **Verification:** Use `show ip route`, `show ip protocols`, `debug ip rip`.

**3.3 The Routing Table**

- **IPv4 Route Entry Components:**
    - **Route Source:** How the route was learned (e.g., C, L, S, R, O, D).
    - **Destination Network:** The address of the remote network.
    - **Administrative Distance:** Trustworthiness of the route source.
    - **Metric:** Value used to determine the best path.
    - **Next Hop:** IP address of the next router to forward the packet to.
    - **Route Timestamp:** How long since the route was last heard from.
    - **Outgoing Interface:** The interface used to forward packets to the destination.
- **IPv4 Routing Table Hierarchy (Classful Concepts - Pre-IOS 15/Classless):**
    - **Level 1 Routes:** Have a subnet mask equal to or less than the classful mask (e.g., network route, supernet route, default route). Can function as a parent route.
    - **Level 2 Routes:** A route that is a subnet of a classful network address (e.g., a subnet route). Always an ultimate route (contains next-hop/exit interface).
    - **Parent Route (Level 1):** A heading indicating the classful network address; does not contain next-hop/exit interface information itself.
    - **Child Route (Level 2):** A specific subnet belonging to the Level 1 parent route.
- **Ultimate Route vs. Parent Route:**
    - **Ultimate Route:** Contains either a next-hop IP or an exit interface (or both). Directly connected, dynamically learned, local, and static routes are usually ultimate routes.
    - **Parent Route:** Does not contain next-hop/exit interface info. It's a heading for Level 2 child routes.
- **Route Lookup Process (IPv4):**
    
    1. Router checks for a Level 1 **best match** (longest match) that is an ultimate route. If found, use it.
    2. If the best match is a Level 1 **parent route**, examine its Level 2 child routes.
    3. If a Level 2 child route matches, use that subnet route (it's the longest match).
    4. If no Level 2 child route matches, continue searching Level 1 supernet or default routes.
    5. If a lower-match Level 1 supernet or default route is found, use it.
    6. If no match is found anywhere, drop the packet.
    
    - **Longest Match Rule:** The route with the most matching high-order bits (longest prefix) is always preferred.
- **IPv6 Routing Table:**
    - Similar components to IPv4.
    - IPv6 is inherently classless, so all routes are effectively Level 1 ultimate routes. There's no concept of Level 1 parent/Level 2 child routes.
    - Lookup is simpler: find the longest prefix match in the table. If found, use it. If not (and no default route), drop the packet.

This summary covers the core concepts from the first three chapters. Remember to refer back to the specific pages cited for the full context and diagrams. Good luck with your studies!




