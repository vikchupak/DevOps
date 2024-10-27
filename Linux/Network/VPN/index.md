- https://www.youtube.com/watch?v=CWy3x3Wux6o
- https://www.geeksforgeeks.org/types-of-virtual-private-network-vpn-and-its-protocols/

There are two main types:

- Site-to-Site vpn
- Remote access vpn (Client-to-Site vpn)
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

Windows
- `ipconfig /all` - list network interfaces
- `route print` - show routing table
