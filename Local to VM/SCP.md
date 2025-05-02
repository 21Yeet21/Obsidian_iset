

### **Step 1: Set Up SSH Server on Rocky Linux**

1. **Install OpenSSH Server** (if not already installed):  
    Rocky Linux uses `dnf` instead of `apt`. Run:
    
    bash
    
    Copy
    
    sudo dnf install openssh-server
    
2. **Start and Enable the SSH Service**:
    
    bash
    
    Copy
    
    sudo systemctl start sshd       # Start the service
    sudo systemctl enable sshd      # Enable on boot
    
3. **Find the VM’s Local IP Address**:  
    Run this command in the VM:
    
    bash
    
    Copy
    
    ip a
    
    Look for the IP under your network interface (e.g., `eth0`, `ens33`). It will resemble `192.168.x.x`.
    

---

### **Step 2: Configure VMware NAT Port Forwarding**

1. **Open VMware Virtual Network Editor** on your Windows host:
    
    - Go to **Edit > Virtual Network Editor**.
        
    - Click **Change Settings** (admin privileges required).
        
2. **Set Up Port Forwarding**:
    
    - Select your NAT network (e.g., `VMnet8`).
        
    - Click **NAT Settings > Add**.
        
    - Configure the rule:
        
        - **Host Port**: `2222` (or any unused port)
            
        - **Guest IP**: Enter the Rocky Linux VM’s IP (from Step 1.3).
            
        - **Guest Port**: `22` (SSH default port).
            
    
    Save the settings.


scp -P 2222 C:\Users\ayoub\Downloads\dns.docx root@localhost:/root/Bureau



### **Middle Ground: Enable SSH Only When Needed**

- **Recommendation**: Keep the port forwarding rule but **disable SSH when unused**.
    
    - Start SSH before transfers:
        
        sudo systemctl start sshd
        
    - Stop SSH afterward:
      
        
        sudo systemctl stop sshd
        

--