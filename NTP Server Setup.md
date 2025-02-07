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