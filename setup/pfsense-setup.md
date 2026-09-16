# pfSense Setup

Configuration guide for the pfSense firewall in the Blue Team SOC Lab.

> **⚠️ Privacy Note:** All IP addresses are masked with asterisks (`*`) to avoid exposing real network information. Replace each `*` with your actual octet values.

## 🔌 Interface Assignment

During installation, assign the network interfaces as follows:

| Interface | VMware Network | IP Address | Role |
| :--- | :--- | :--- | :--- |
| **WAN (em0)** | NAT | 192.168.168.* (DHCP) | Internet access |
| **OPT1 (em1)** | VMnet2 | 192.168.10.*/24 | Attacker network |
| **LAN (em2)** | VMnet3 | 192.168.20.*/24 | Victim network |

> **Note:** The interface names (`em0`, `em1`, `em2`) may vary. Use the MAC addresses to identify the correct adapters.

## 🌐 WAN Configuration

1. Go to **Interfaces → WAN**.
2. Set **IPv4 Configuration Type** to **DHCP**.
3. Leave **Block private networks** and **Block bogon networks** unchecked.
4. Click **Save** → **Apply Changes**.

## 🏠 LAN Configuration

1. Go to **Interfaces → LAN**.
2. Set **IPv4 Configuration Type** to **Static IPv4**.
3. Set **IPv4 Address** to `192.168.20.*` with a **/24** subnet mask.
4. Click **Save** → **Apply Changes**.

## 🔒 OPT1 Configuration

1. Go to **Interfaces → OPT1**.
2. Check **Enable Interface**.
3. Set **IPv4 Configuration Type** to **Static IPv4**.
4. Set **IPv4 Address** to `192.168.10.*` with a **/24** subnet mask.
5. Click **Save** → **Apply Changes**.

## 📡 DHCP Server Configuration

### LAN (Victim Network)
1. Go to **Services → DHCP Server → LAN**.
2. Check **Enable DHCP server on LAN interface**.
3. Set **Range** from `192.168.20.*` to `192.168.20.*` (example: `.100` to `.200`).
4. Set **DNS Servers** to `8.8.8.8, 8.8.4.4`.
5. Click **Save** → **Apply Changes**.

### OPT1 (Attacker Network)
1. Go to **Services → DHCP Server → OPT1**.
2. Check **Enable DHCP server on OPT1 interface**.
3. Set **Range** from `192.168.10.*` to `192.168.10.*` (example: `.100` to `.200`).
4. Set **DNS Servers** to `8.8.8.8, 8.8.4.4`.
5. Click **Save** → **Apply Changes**.

## 🔥 Firewall Rules

### LAN (Victim Network)
1. Go to **Firewall → Rules → LAN**.
2. Add a rule:
   - **Action:** Pass
   - **Protocol:** Any
   - **Source:** LAN subnets
   - **Destination:** Any
3. Click **Save** → **Apply Changes**.

### OPT1 (Attacker Network)
1. Go to **Firewall → Rules → OPT1**.
2. Add a rule:
   - **Action:** Pass
   - **Protocol:** Any
   - **Source:** OPT1 net
   - **Destination:** Any
3. Click **Save** → **Apply Changes**.

> **Important:** This rule allows the attacker (Linux Mint) to reach the victim (Windows 10) and the internet. Without it, attacks will be blocked.

## 🌍 NAT (Outbound)

1. Go to **Firewall → NAT → Outbound**.
2. Select **Automatic outbound NAT rule generation**.
3. Click **Save** → **Apply Changes**.

## 🔑 Default Credentials

| Access | URL | Username | Password |
| :--- | :--- | :--- | :--- |
| **WebGUI** | `https://192.168.20.*` | `admin` | `pfsense` |

> **Change the default password immediately after first login.**


