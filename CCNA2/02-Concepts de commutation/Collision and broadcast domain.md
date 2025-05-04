
## 2.2.1 Collision Domains

- **Collision domain**:  
    A network segment where devices share the same bandwidth and can cause collisions when transmitting at the same time.
    
- **Legacy hubs**:  
    Devices compete for the shared medium, increasing collision risk.
    
- **Switch behavior**:
    
    - Each **switch port** in **half-duplex** is a separate collision domain.
        
    - In **full-duplex**, collisions **do not occur**.
        
    - Switch ports **autonegotiate** full-duplex if the connected device supports it.
        
    - If connected to a **half-duplex device** (e.g., legacy hub), the switch port operates in half-duplex and participates in a collision domain.
        
- **Key point**:  
    Full-duplex and highest common bandwidth are selected when both devices support it.
    


---

## 2.2.2 Broadcast Domains

- **Broadcast domain**:  
    A group of interconnected switches where broadcast frames are forwarded to all devices.
    
- **Separation of broadcast domains**:
    
    - Only **network layer devices** (e.g., **routers**) can divide Layer 2 broadcast domains.
        
    - Routers segment **both** collision and broadcast domains.
        
- **Layer 2 broadcast**:
    
    - Destination **MAC address** is set to **all binary ones** (FF:FF:FF:FF:FF:FF).
        
    - Called the **MAC broadcast domain**.
        
- **MAC broadcast domain**:  
    All devices on the LAN that receive broadcast frames from a sender.
    
---

## 2.2.3 Alleviate Network Congestion

- **Full-duplex links**:  
    Switch ports try to establish full-duplex by default, eliminating collisions and giving full bandwidth to connected devices.
    
- **Switch functions**:
    
    - Interconnect LAN segments.
        
    - Use MAC address tables to decide forwarding.
        
    - Reduce or eliminate collisions.
        
- **Key characteristics that reduce congestion**:
    
    - **Fast port speeds**:  
        Access switches (100 Mbps, 1 Gbps), distribution switches (100 Mbps, 1 Gbps, 10 Gbps), core/data center switches (10 Gbps, 40 Gbps, 100 Gbps).
        
    - **Fast internal switching**:  
        High-speed internal bus or shared memory for better performance.
        
    - **Large frame buffers**:  
        Temporary storage of more frames to avoid dropping when switching between ports of different speeds.
        
    - **High port density**:  
        Fewer switches needed, keeping traffic local and reducing congestion.
        

---
