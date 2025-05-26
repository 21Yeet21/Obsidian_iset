Okay, I can help you with the commands for your VoIP mini-project in Packet Tracer. Based on your document "Travail demandé.docx", you'll be configuring a Cisco 2811 router and a Cisco 3560 switch.

Here's a breakdown of the configuration steps and the typical commands you'll need. Remember to adapt IP addresses to your specific network plan if they differ from the common examples.

**Project Requirements Summary:**

- **Devices:** Cisco 2811 Router, Cisco 3560 Switch
- **VLANs:**
    - VLAN 10: Data (for PCs)
    - VLAN 20: Voice (for IP Phones)
- **DHCP:** Router will act as DHCP server for both VLANs.
- **Goal:** PCs and IP Phones get IPs from DHCP, IP phones register, and communication is successful between PCs and between IP phones.

---

### **I. Cisco 2811 Router Configuration**

The router will handle:

- Inter-VLAN routing (allowing PCs and Phones on different VLANs to communicate if needed, though your primary goal is PC-to-PC and Phone-to-Phone on their respective services).
- DHCP services for both VLANs.
- Telephony services (CallManager Express - CME) for the IP Phones.

Let's assume your router's FastEthernet0/0 interface will connect to the switch. We'll use sub-interfaces for each VLAN.

**1. Configure Sub-interfaces for VLANs:**

Cisco CLI

```
enable
configure terminal

! Interface for Data VLAN (VLAN 10)
interface FastEthernet0/0.10
 encapsulation dot1Q 10
 ip address 192.168.10.1 255.255.255.0  ! Gateway for Data VLAN
 no shutdown

! Interface for Voice VLAN (VLAN 20)
interface FastEthernet0/0.20
 encapsulation dot1Q 20
 ip address 192.168.20.1 255.255.255.0  ! Gateway for Voice VLAN
 no shutdown

! Bring up the physical interface
interface FastEthernet0/0
 no shutdown
exit
```

**2. Configure DHCP Pools:**

Cisco CLI

```
! DHCP Pool for Data VLAN (PCs)
ip dhcp pool DATA_POOL
 network 192.168.10.0 255.255.255.0
 default-router 192.168.10.1
 dns-server 8.8.8.8             ! Optional: You can use your ISP's or any public DNS

! DHCP Pool for Voice VLAN (IP Phones)
ip dhcp pool VOICE_POOL
 network 192.168.20.0 255.255.255.0
 default-router 192.168.20.1
 option 150 ip 192.168.20.1     ! This tells phones where the TFTP server (CME router) is
 dns-server 8.8.8.8             ! Optional
exit
```

- **Note:** `option 150` is crucial for Cisco IP phones to find the CallManager Express for configuration and registration. The IP address `192.168.20.1` is the router's IP on the voice VLAN, which will also serve as the TFTP server for the phones.

**3. Configure Telephony Service (CallManager Express - CME):**

This part enables the router to act as a basic phone system.

Cisco CLI

```
telephony-service
 max-ephones 4                ! Maximum number of IP phones you plan to use (as per your topology)
 max-dn 4                     ! Maximum directory numbers (lines)
 ip source-address 192.168.20.1 port 2000 ! Tells phones which IP and port to register to
 auto assign 1 to 4           ! Automatically assign extension numbers to phones as they register
 create cnf-files             ! Creates configuration files for the phones
 no shutdown
exit

! Configure directory numbers (extensions) for the phones
! You need to create one ephone-dn for each phone line/extension

! For IP Phone0 (Number: 1004 in your diagram)
ephone-dn 1
 number 1004
exit

! For IP Phone1 (Number: 1003 in your diagram)
ephone-dn 2
 number 1003
exit

! For IP Phone2 (Number: 1001 in your diagram)
ephone-dn 3
 number 1001
exit

! For IP Phone3 (Number: 1002 in your diagram)
ephone-dn 4
 number 1002
exit
```

- **Important:** The phone numbers (1004, 1003, 1001, 1002) are taken from your "Travail demandé.docx" diagram. You assign these numbers to `ephone-dn` (directory number) entries. The `auto assign 1 to 4` command under `telephony-service` will link the first phone that registers to `ephone-dn 1`, the second to `ephone-dn 2`, and so on.

---

### **II. Cisco 3560 Switch Configuration**

The switch will:

- Separate traffic into Data and Voice VLANs.
- Connect PCs to the Data VLAN.
- Connect IP Phones to the Voice VLAN (while also allowing the PC connected through the phone to use the Data VLAN).
- Trunk to the router to carry traffic for both VLANs.

Let's assume:

- FastEthernet0/1 will connect to the Router.
- FastEthernet0/2 to FastEthernet0/5 will connect to your IP Phone + PC setups.

**1. Create VLANs:**

Cisco CLI

```
enable
configure terminal

vlan 10
 name DATA
exit

vlan 20
 name VOICE
exit
```

**2. Configure the Trunk Port to the Router:**

This port needs to carry traffic for both VLAN 10 and VLAN 20.

Cisco CLI

```
interface FastEthernet0/1   ! Or whichever port connects to your router
 switchport trunk encapsulation dot1q  ! (May not be needed if it's the default, but good practice)
 switchport mode trunk
 switchport trunk allowed vlan 10,20
 no shutdown
exit
```

**3. Configure Access Ports for IP Phones and PCs:**

Cisco IP phones have a built-in mini-switch. The port on the 3560 switch will be an access port for the Data VLAN, but it will also instruct the IP phone (via CDP - Cisco Discovery Protocol) to tag its voice traffic for the Voice VLAN.

Cisco CLI

```
! Example for one port (repeat for all ports connected to IP Phones: Fa0/2, Fa0/3, Fa0/4, Fa0/5)
interface FastEthernet0/2    ! Port connected to IP Phone0 + PC0
 switchport mode access
 switchport access vlan 10      ! Data VLAN for the PC connected through the phone
 switchport voice vlan 20     ! Voice VLAN for the IP Phone
 spanning-tree portfast       ! Optional: helps ports come up faster, use on access ports only
 no shutdown
exit

interface FastEthernet0/3    ! Port connected to IP Phone1 + PC1
 switchport mode access
 switchport access vlan 10
 switchport voice vlan 20
 spanning-tree portfast
 no shutdown
exit

interface FastEthernet0/4    ! Port connected to IP Phone2 + PC2
 switchport mode access
 switchport access vlan 10
 switchport voice vlan 20
 spanning-tree portfast
 no shutdown
exit

interface FastEthernet0/5    ! Port connected to IP Phone3 + PC3
 switchport mode access
 switchport access vlan 10
 switchport voice vlan 20
 spanning-tree portfast
 no shutdown
exit
```

- The `switchport voice vlan 20` command is key here. It tells the switch to expect voice traffic tagged for VLAN 20 from the Cisco IP phone. The phone itself will tag its voice packets for VLAN 20, and pass through untagged data traffic from the connected PC, which the switch will then place onto VLAN 10.

---

### **III. Packet Tracer Specifics**

- **Power on IP Phones:** In Packet Tracer, IP phones often need to be manually powered on. Click on the IP phone, go to the 'Physical' tab, and drag the power adapter to the power port on the phone.
- **DHCP on PCs:** Ensure the PCs in Packet Tracer are set to obtain IP addresses via DHCP in their IP Configuration settings.
- **Phone Registration:** After configuring the router and switch, the IP phones should boot up, request an IP from the VOICE_POOL via DHCP, receive the `option 150` pointing to the router, download their configuration, and register with the CME on the router. You should see their assigned extension numbers appear on their screens.
- **Testing:**
    - **PCs:** Ping between PCs. They should get IPs in the `192.168.10.x` range.
    - **IP Phones:** Try calling from one IP phone to another using their assigned extension numbers (e.g., dial 1003 from phone 1004).

---

**Important Commands for Verification:**

**On the Router:**

- `show ip dhcp binding`: See which IP addresses have been leased out.
- `show ip interface brief`: Check status and IP addresses of interfaces and sub-interfaces.
- `show ephone`: Check the registration status of IP phones.
- `show ephone-dn`: Check the status of directory numbers.
- `show telephony-service`: View the telephony service configuration.

**On the Switch:**

- `show vlan brief`: See configured VLANs and port assignments.
- `show interfaces trunk`: Check trunk port status.
- `show interfaces <interface_name> switchport`: Detailed information about a specific switch port (e.g., `show interfaces FastEthernet0/2 switchport`).
- `show cdp neighbors`: Useful to see if the switch is detecting the IP phones and router.

This should give you a solid foundation for your VoIP configuration in Packet Tracer. Let me know if you encounter any specific issues as you go through the setup!