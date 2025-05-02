  

This title covers:  
- **SSH vs. Telnet**: Why SSH is preferred for secure remote access.  
- **SSH Configuration**: Step-by-step setup on a Cisco switch.  
- **Verification**: Ensuring SSH is operational and secure.  



### **Detailed Summary of the Section**  

---

#### **1.3.1 Telnet Operation**  
- **Telnet**:  
  - Uses **TCP port 23**.  
  - Transmits data (including usernames and passwords) in **plaintext**.  
  - **Security Risk**: Vulnerable to packet sniffing (e.g., Wireshark can capture credentials).  
  - **Example**: A threat actor captures the username `admin` and password `ccna` from a Telnet session.  

**Key Takeaway**: Avoid using Telnet for remote access due to its lack of encryption.  

---

#### **1.3.2 SSH Operation**  
- **SSH (Secure Shell)**:  
  - Uses **TCP port 22**.  
  - Provides **encrypted** communication for both authentication and data transmission.  
  - **Security**: Protects against eavesdropping and credential theft.  
  - **Example**: Wireshark captures an SSH session, but credentials and data are encrypted.  

**Key Takeaway**: Always use SSH instead of Telnet for secure remote access.  

---

#### **1.3.3 Verify Switch Supports SSH**  
- **Requirement**: The switch must run an IOS image with cryptographic features (indicated by `k9` in the filename).  
- **Command**:  
  ```  
  S1# show version  
  ```  
  - Example Output:  
    ```  
    Cisco IOS Software, C2960 Software (C2960-LANBASEK9-M), Version 15.0(2)SE7  
    ```  
  - **Key Info**: Look for `k9` in the IOS filename (e.g., `C2960-LANBASEK9-M`).  

**Key Takeaway**: Ensure the switch runs a `k9` IOS image to support SSH.  

---

#### **1.3.4 SSH Configuration**  
Follow these steps to configure SSH on a Cisco switch:  

### **How to Log in to the Router Using SSH**

After configuring SSH on the router, you can log in using an SSH client (such as **PuTTY**, **OpenSSH**, or **SecureCRT**) from another device. Here’s how:

1. **Using Linux/macOS (Terminal):**
    
    ```bash
    ssh admin@<router-ip>
    ```
    
    Example:
    
    ```bash
    ssh admin@192.168.1.1
    ```
    
    - It will prompt for a password. Enter `ccna` (set in `username admin secret ccna`).
2. **Using Windows (PuTTY):**
    
    - Open PuTTY.
    - Enter the router’s IP address (e.g., `192.168.1.1`).
    - Select **SSH** as the connection type.
    - Click **Open** and log in with:
        - **Username**: `admin`
        - **Password**: `ccna`

---

### **Explanation of the Commands**

#### **1. Check if SSH is Enabled**

```bash
S1# show ip ssh
```

- Verifies if SSH is configured and running.

#### **2. Set a Domain Name**

```bash
S1(config)# ip domain-name cisco.com
```

- Required for generating RSA encryption keys.
- The domain name is part of the SSH key generation process.

#### **3. Generate RSA Keys**

```bash
S1(config)# crypto key generate rsa
```

- Generates cryptographic keys for SSH encryption.
- It will prompt for a key size (minimum **1024 bits**, recommended **2048 bits**).

#### **4. Create a Local User Account**

```bash
S1(config)# username admin secret ccna
```

- Creates a user `admin` with an encrypted password `ccna`.
- The `secret` keyword ensures stronger encryption compared to `password`.

#### **5. Configure Virtual Terminal (VTY) Lines**

```bash
S1(config)# line vty 0 15
```

- Selects **VTY lines 0 to 15**, allowing up to **16 simultaneous SSH sessions**.

#### **6. Enable SSH Access Only**

```bash
S1(config-line)# transport input ssh
```

- Restricts remote access to **only SSH** (disables Telnet for security).

#### **7. Enable Local Authentication**

```bash
S1(config-line)# login local
```

- Requires users to authenticate with **locally stored credentials** (`admin` and `ccna`).

#### **8. Set SSH Version 2**

```bash
S1(config)# ip ssh version 2
```

- Enables **SSHv2**, which is more secure than SSHv1.

---

Now, the router is accessible via SSH using the configured credentials.

---

#### **1.3.5 Verify SSH is Operational**  
- **SSH Client**: Use tools like **PuTTY** to connect to the switch.  
- **Example Configuration**:  
  - Switch SVI IP: `172.17.99.11`  
  - PC IP: `172.17.99.21`  
  - PuTTY Settings:  
    - Host: `172.17.99.11`  
    - Port: `22`  
    - Connection Type: SSH  

- **Login Prompt**:  
  ```  
  Login as: admin  
  Password: ccna  
  ```  

- **Verification Commands**:  
  - Check SSH status:  
    ```  
    S1# show ip ssh  
    ```  
    Example Output:  
    ```  
    SSH Enabled - version 2.0  
    Authentication timeout: 120 secs; Authentication retries: 3  
    ```  
  - Check active SSH connections:  
    ```  
    S1# show ssh  
    ```  
    Example Output:  
    ```  
    Connection Version Mode Encryption  Hmac                State          Username  
    0          2.0     IN   aes256-cbc  hmac-sha1    Session started       admin  
    ```  

**Key Takeaway**: Use `show ip ssh` and `show ssh` to verify SSH configuration and active sessions.  

---

### **Key Takeaways**  
- **SSH vs. Telnet**: SSH is secure; Telnet is not. Always use SSH for remote access.  
- **SSH Configuration**:  
  - Requires a `k9` IOS image.  
  - Steps: Domain name, RSA keys, user authentication, VTY line configuration, and SSH version 2.  
- **Verification**: Use `show ip ssh` and `show ssh` to confirm SSH is operational.  

Let me know if you need further refinements or additional details! 🔧🔍