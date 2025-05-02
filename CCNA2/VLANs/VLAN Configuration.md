**VLAN Creation Commands**

- VLAN configuration is stored in **`vlan.dat`** in flash memory (persistent).
    
- Running `copy running-config startup-config` is **recommended**, though not required for VLANs alone.
    
- It's best practice to **name VLANs** during creation for clarity.
    

| **Task**                        | **IOS Command**                       |
| ------------------------------- | ------------------------------------- |
| Enter global configuration mode | `Switch# configure terminal`          |
| Create a VLAN with a valid ID   | `Switch(config)# vlan vlan-id`        |
| Name the VLAN                   | `Switch(config-vlan)# name vlan-name` |
| Exit to privileged EXEC mode    | `Switch(config-vlan)# end`            |

### VLAN Port Assignment Commands

Assigning ports to VLANs ensures that connected devices are part of the correct broadcast domain. Using access mode prevents trunk negotiation for better security.

| **Task**                    | **IOS Command**                                     |
| --------------------------- | --------------------------------------------------- |
| Enter interface config mode | `Switch(config)# interface interface-id`            |
| Set port to access mode     | `Switch(config-if)# switchport mode access`         |
| Assign port to VLAN         | `Switch(config-if)# switchport access vlan vlan-id` |
| Exit to exec mode           | `Switch(config-if)# end`                            |

### Data and Voice VLANs

A single access port can support both a **data VLAN** (for end devices like PCs) and a **voice VLAN** (for IP phones), enabling efficient traffic separation and QoS handling.


![[Pasted image 20250502154940.png]]

### Data and Voice VLAN Example

To support both data and voice traffic on a single switch port (e.g., when connecting an IP phone and a PC), you configure the port with two VLANs:

- **Data VLAN**: Assigned using `switchport access vlan`.
    
- **Voice VLAN**: Assigned using `switchport voice vlan`.
    

Additionally, **QoS (Quality of Service)** must be enabled to prioritize voice traffic, which is delay-sensitive. This is done with the command `mls qos trust cos`, which tells the switch to trust the **Class of Service (CoS)** markings added by the IP phone.

**Key Commands:**

- `switchport mode access`: Puts the interface in access mode.
    
- `switchport access vlan 20`: Assigns the data VLAN.
    
- `switchport voice vlan 150`: Assigns the voice VLAN.
    
- `mls qos trust cos`: Enables QoS trusting of CoS values from the IP phone.
    

Note: If a VLAN (e.g., VLAN 30) is assigned to an interface and doesn't exist, the switch will automatically create it.

This setup is essential for ensuring that voice traffic gets the appropriate priority in mixed traffic environments.

### Verify VLAN Information

After VLANs are created, use the `show vlan` command to verify their configuration. You can add options to this command for more specific output.

|**Command Option**|**Description**|
|---|---|
|`brief`|Shows VLAN ID, name, status, and assigned ports (one line per VLAN).|
|`id vlan-id`|Displays detailed info about a specific VLAN by its ID.|
|`name vlan-name`|Displays detailed info about a specific VLAN by its name.|
|`summary`|Gives a summary of VLAN configuration and usage.|

These commands help ensure VLANs are correctly configured and operational.


### Change VLAN Port Membership

Changing the VLAN port membership can be done in several ways.

- To correct the VLAN assignment, use the `switchport access vlan vlan-id` command on the specific interface. For example, to assign Fa0/18 to VLAN 20, use:
    
    ```
    S1(config)# interface fa0/18
    S1(config-if)# switchport access vlan 20
    ```
    
- If you need to revert the port to the default VLAN (VLAN 1), use the `no switchport access vlan` command:
    
    ```
    S1(config)# interface fa0/18
    S1(config-if)# no switchport access vlan
    ```
    
- After running the command, use `show vlan brief` to confirm the updated VLAN membership. For example:
    
    ```
    S1# show vlan brief
    VLAN Name                 Status    Ports
    ---- ------------------ --------- -------------------------------
    1    default            active    Fa0/1, Fa0/2, Fa0/3, Fa0/4
                                      ...
    20   student            active    
    ```
    
- You can also verify the port configuration with `show interfaces fa0/18 switchport`:
    
    ```
    S1# show interfaces fa0/18 switchport
    Name: Fa0/18
    Switchport: Enabled
    Administrative Mode: static access
    Operational Mode: static access
    Access Mode VLAN: 1 (default)
    ```
    

This command ensures that the port is correctly assigned to the desired VLAN or reverted to VLAN 1.


### Delete VLANs

Remove data from port 

```
no switchport access vlan
```

To delete a VLAN, use the following command in global configuration mode:

- **Remove a VLAN:**
    
    ```
    S1(config)# no vlan vlan-id
    ```
    
- **Warning:** Before deleting a VLAN, ensure all member ports are reassigned to another active VLAN. If ports remain in a deleted VLAN, they will lose connectivity until reassigned.
    

To remove all VLAN configurations, you can delete the entire `vlan.dat` file:

- **Delete the vlan.dat file:**
    
    ```
    S1# delete flash:vlan.dat
    ```
    
- **For switches in their default location:**
    
    ```
    S1# delete vlan.dat
    ```
    

After this, reload the switch to clear all VLAN configurations, returning it to its factory default state.

- **To fully reset the switch to factory defaults:**
    
    1. Unplug all cables except the console and power.
        
    2. Enter:
        
    
    ```
    S1# erase startup-config
    S1# delete vlan.dat
    ```
    

This restores the switch to its default configuration, including the VLAN settings.