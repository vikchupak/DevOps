# When requests fails, possible reasons of the problem

- No Internet Connection
- DNS settings
- Routing table issues
- Firewall settings (Blocking Requests)
- VPN or Proxy settings
- Server-Side Issues or IP Whitelisting

## **1. No Internet Connection**
- **Symptoms**: No response from any website or IP.
- **Causes**:
  - Disconnected from Wi-Fi/Ethernet.
  - Router/modem is down.
  - ISP issues.
  - Network adapter is disabled.

**🛠 Fixes:**
- Check network status: `nmcli device status`
- Restart networking:  
  ```sh
  sudo systemctl restart NetworkManager
  ```
- Try another network.

---

## **2. DNS Resolution Failure**
- **Symptoms**: Error like `Could not resolve host`
- **Causes**:
  - No DNS server configured.
  - DNS server is down.
  - Corrupt `/etc/resolv.conf`.

**🛠 Fixes:**
- Test resolving the domain manually with current DNS
  ```bash
  nslookup <some.domain.com>
  # If it fails, your DNS server may not be working
  ```
- Test resolving the domain manually with another DNS (Google dns)
    ```bash
  nslookup <some.domain.com> 8.8.8.8
  ```
- Check DNS settings:  
  ```sh
  cat /etc/resolv.conf
  ```
- Manually set a DNS:  
  ```sh
  echo "nameserver 8.8.8.8" | sudo tee /etc/resolv.conf
  ```
- Restart DNS resolver:  
  ```sh
  sudo systemctl restart systemd-resolved
  ```

### **Fallback DNS**

The **fallback DNS** is typically used when the primary DNS server (such as the one assigned by the VPN) is unreachable or cannot resolve a domain. If you have configured a fallback DNS, here’s where you can check:

---

### **1️⃣ Check `/etc/resolv.conf`**

On Linux, the `/etc/resolv.conf` file holds the list of DNS servers your system is using, including any fallback DNS.

```sh
cat /etc/resolv.conf
```

- **Primary DNS** will be the first `nameserver` listed.
- **Fallback DNS** (if any) will appear as a second or subsequent `nameserver`.

For example:
```plaintext
nameserver 10.10.10.1   # Primary (VPN DNS)
nameserver 8.8.8.8      # Fallback (Google DNS)
```

- If the VPN DNS is down, the system will use `8.8.8.8` for DNS resolution.

### **3️⃣ Check NetworkManager (If Using NetworkManager)**

If you're using **NetworkManager** to manage your network connections, you can use `nmcli` to check the DNS settings:

```sh
nmcli device show | grep DNS
```

This will show the DNS servers for all network interfaces, including the VPN connection.

Example output:
```plaintext
IP4.DNS[1]:                         10.10.10.1   # VPN DNS
IP4.DNS[2]:                         8.8.8.8      # Fallback DNS (Google)
```
---

### **5️⃣ Check for DNS Leak Test (Web or Command Line)**

To see if fallback DNS is being used during a DNS resolution failure:

#### **Web-based Test:**
- Go to a DNS leak test site, such as [dnsleaktest.com](https://dnsleaktest.com), and run the test. If you see multiple DNS servers listed, one of them might be your fallback DNS.

---

## **3. Network Routing Issues**
- **Symptoms**: Cannot reach specific hosts but can ping `8.8.8.8`.
- **Causes**:
  - Incorrect gateway.
  - Misconfigured static routes.
  - VPN issues.

**🛠 Fixes:**
- Check routing table:  
  ```sh
  ip route
  ```
- Add missing default gateway:
  ```sh
  sudo ip route add default via <GATEWAY_IP>
  ```

---

## **4. Firewall Blocking Requests**
- **Symptoms**: Connection refused, no response.
- **Causes**:
  - Local firewall (`iptables`, `ufw`) blocking requests.
  - Corporate or ISP-level firewall.
  - VPN restrictions.

**🛠 Fixes:**
- Check firewall rules:  
  ```sh
  sudo iptables -L
  ```
- Temporarily disable firewall:
  ```sh
  sudo systemctl stop ufw
  ```

---

## **5. VPN or Proxy Interference**
- **Symptoms**: Some sites work, others don’t.
- **Causes**:
  - VPN assigns wrong DNS (e.g., `/32` vs `/23` subnet mask issue).
  - Proxy misconfiguration.

**🛠 Fixes:**
- Check VPN settings:  
  ```sh
  ip a | grep tun
  ```
- Disable VPN and test:
  ```sh
  sudo systemctl stop openconnect
  ```

---

## **6. Server-Side Issues**
- **Symptoms**: Only one site is unreachable.
- **Causes**:
  - Website is down.
  - Server blocking your IP.

**🛠 Fixes:**
- Try a different website.
- Check if the site is down:  
  ```sh
  curl -Is https://example.com | head -n 1
  ```

---

### **Summary**
| Issue                 | Command to Diagnose                  | Possible Fix |
|----------------------|-----------------------------------|-------------|
| **No internet**        | `ping -c 4 8.8.8.8`               | Check router, ISP |
| **DNS failure**        | `nslookup google.com`            | Set DNS manually |
| **Routing problem**    | `ip route`                      | Add gateway route |
| **Firewall blocking**  | `sudo iptables -L`              | Disable firewall |
| **VPN interference**   | `ip a | grep tun`               | Disable VPN |
| **Server down**        | `curl -Is https://example.com`  | Wait or try another server |
