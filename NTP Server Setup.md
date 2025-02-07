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