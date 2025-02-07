# Setting Up an NTP Server and Client with Chrony

## **Step 1: Configure the NTP Source Server (Primary Server)**
This server will act as the authoritative time source for the client.

### **1. Install Chrony**
```bash
sudo apt update
sudo apt install chrony -y  # Ubuntu/Debian
```
<button onclick="navigator.clipboard.writeText('sudo apt update\nsudo apt install chrony -y')">📋 Copy</button>

```bash
sudo yum install chrony -y  # CentOS/RHEL
```
<button onclick="navigator.clipboard.writeText('sudo yum install chrony -y')">📋 Copy</button>

### **2. Configure Chrony as an NTP Server**
Edit the configuration file:
```bash
sudo nano /etc/chrony/chrony.conf
```
<button onclick="navigator.clipboard.writeText('sudo nano /etc/chrony/chrony.conf')">📋 Copy</button>

Make the following changes:

- **Comment out external NTP sources**
  ```bash
  # pool 0.centos.pool.ntp.org iburst
  ```
<button onclick="navigator.clipboard.writeText('# pool 0.centos.pool.ntp.org iburst')">📋 Copy</button>

- **Allow the client machine to access this server** (Replace `192.168.1.0/24` with your actual network range):
  ```bash
  allow 192.168.1.0/24
  ```
<button onclick="navigator.clipboard.writeText('allow 192.168.1.0/24')">📋 Copy</button>

- **Enable local clock as a fallback option**
  ```bash
  local stratum 10
  ```
<button onclick="navigator.clipboard.writeText('local stratum 10')">📋 Copy</button>

- **Ensure `makestep` is set to correct large offsets quickly**
  ```bash
  makestep 1.0 3
  ```
<button onclick="navigator.clipboard.writeText('makestep 1.0 3')">📋 Copy</button>

### **3. Restart Chrony and Enable It**
```bash
sudo systemctl restart chronyd
sudo systemctl enable chronyd
```
<button onclick="navigator.clipboard.writeText('sudo systemctl restart chronyd\nsudo systemctl enable chronyd')">📋 Copy</button>

### **4. Open Firewall for NTP (If Enabled)**
```bash
sudo ufw allow 123/udp  # Ubuntu/Debian
```
<button onclick="navigator.clipboard.writeText('sudo ufw allow 123/udp')">📋 Copy</button>

```bash
sudo firewall-cmd --add-service=ntp --permanent  # CentOS/RHEL
sudo firewall-cmd --reload
```
<button onclick="navigator.clipboard.writeText('sudo firewall-cmd --add-service=ntp --permanent\nsudo firewall-cmd --reload')">📋 Copy</button>

### **5. Verify That the Server Is Working**
```bash
chronyc sources -v
```
<button onclick="navigator.clipboard.writeText('chronyc sources -v')">📋 Copy</button>

Check that the service is listening on port `123`:
```bash
sudo ss -ulpn | grep 123
```
<button onclick="navigator.clipboard.writeText('sudo ss -ulpn | grep 123')">📋 Copy</button>

---

## **Step 2: Configure the Syncing Client (Secondary Server)**

### **1. Install Chrony on the Client**
```bash
sudo apt update
sudo apt install chrony -y  # Ubuntu/Debian
```
<button onclick="navigator.clipboard.writeText('sudo apt update\nsudo apt install chrony -y')">📋 Copy</button>

```bash
sudo yum install chrony -y  # CentOS/RHEL
```
<button onclick="navigator.clipboard.writeText('sudo yum install chrony -y')">📋 Copy</button>

### **2. Configure Chrony to Sync from the Primary Server**
Edit the client’s `chrony.conf`:
```bash
sudo nano /etc/chrony/chrony.conf
```
<button onclick="navigator.clipboard.writeText('sudo nano /etc/chrony/chrony.conf')">📋 Copy</button>

Replace or add:
```bash
server 192.168.1.100 iburst  # Replace with your NTP server's IP
```
<button onclick="navigator.clipboard.writeText('server 192.168.1.100 iburst')">📋 Copy</button>

### **3. Restart Chrony**
```bash
sudo systemctl restart chronyd
sudo systemctl enable chronyd
```
<button onclick="navigator.clipboard.writeText('sudo systemctl restart chronyd\nsudo systemctl enable chronyd')">📋 Copy</button>

### **4. Verify That the Client Is Syncing**
Run:
```bash
chronyc sources -v
```
<button onclick="navigator.clipboard.writeText('chronyc sources -v')">📋 Copy</button>

Check sync status:
```bash
chronyc tracking
```
<button onclick="navigator.clipboard.writeText('chronyc tracking')">📋 Copy</button>

---

## **Step 3: Testing & Troubleshooting**

1. **Check if Chrony is running properly:**
   ```bash
   sudo systemctl status chronyd
   ```
   <button onclick="navigator.clipboard.writeText('sudo systemctl status chronyd')">📋 Copy</button>

2. **Force a manual sync on the client:**
   ```bash
   sudo chronyc makestep
   ```
   <button onclick="navigator.clipboard.writeText('sudo chronyc makestep')">📋 Copy</button>

3. **Check logs for errors:**
   ```bash
   sudo journalctl -u chronyd --no-pager | tail -50
   ```
   <button onclick="navigator.clipboard.writeText('sudo journalctl -u chronyd --no-pager | tail -50')">📋 Copy</button>

---