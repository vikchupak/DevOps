- https://www.youtube.com/watch?v=CWy3x3Wux6o
- https://www.geeksforgeeks.org/types-of-virtual-private-network-vpn-and-its-protocols/

There are two main types:

- Site-to-Site vpn
  - Description
    - Permanent. Connects entire networks to each other. It is typically used by organizations with multiple fixed locations (like a headquarters and a branch office) to allow them to communicate over the public internet as if they were on the same local network
    - A VPN gateway (router or firewall) at Location A establishes a permanent "tunnel" with a gateway at Location B
    - User Experience is transparent. Employees at the branch office don’t need to "log in" to the VPN; they just access files on the HQ server as if the server were in the next room
- Remote access vpn (Client-to-Site vpn)
  - Description
    - Temporary. Connects individual devices to a network. This is the "Work from Home" special
    - An individual user installs VPN software (a "client") on their laptop or phone. They manually "dial in" to the corporate VPN gateway to gain access
    - User Experience is "on-demand". The user must authenticate (usually with MFA) to establish the connection. Once they disconnect, they no longer have access to the internal network
  - Configuration types
    - Full tunnel (all traffic from host/client passes through vpn)
      ![image](https://github.com/user-attachments/assets/c5848fae-ebdb-4e05-aaef-26f44a961de1)
    - Split tunnel (only traffic addressed to corporate network passes through vpn)
      ![Screenshot from 2024-10-27 14-07-00](https://github.com/user-attachments/assets/75a5d737-3dc2-40ab-b661-49bc25df200b)

Linux
- `ip addr` - list network interfaces
- `ip route` - show routing table\
  Show routing table with better formatting
  ```
  echo -e "Destination\tGateway\tNetmask\tFlags\tMetric\tRef\tUse\tIface\n$(ip route | awk '{print $1, $3, $5, $6, $7, $8, $9, $10}')" | column -t
  ```
  ```
  route -n
  ```

Windows
- `ipconfig /all` - list network interfaces
- `route print` - show routing table
