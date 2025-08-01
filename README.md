# Static Routing Project

## 1. Network Topology
The topology consists of **3 Routers**, **2 PCs**, and **1 Server**, connected as follows:

- **Router0** <-> **Router1** <-> **Router2**
- Each router is connected to a different LAN subnet.
- Static Routing is configured to allow end-to-end communication.

```
PC0 (192.168.1.10) ---- Router0 ---- Router1 ---- Router2 ---- Server (192.168.100.10)
                             |          |          |
                     192.168.1.0/24  172.16.0.0/24 192.168.100.0/24
```

## 2. IP Addressing Table

| Device      | Interface            | IP Address        | Subnet Mask       |
|------------ |--------------------- |----------------- |----------------- |
| Router0     | G0/0                 | 10.0.0.1         | 255.255.255.252  |
|             | G0/1                 | 192.168.1.1      | 255.255.255.0    |
|             | G0/2                 | 12.0.0.1         | 255.255.255.252  |
| Router1     | G0/0                 | 10.0.0.2         | 255.255.255.252  |
|             | G0/1                 | 172.16.0.10      | 255.255.255.0    |
|             | G0/2                 | 11.0.0.2         | 255.255.255.252  |
| Router2     | G0/0                 | 11.0.0.1         | 255.255.255.252  |
|             | G0/1                 | 12.0.0.2         | 255.255.255.252  |
|             | G0/2                 | 192.168.100.1    | 255.255.255.0    |
| PC0         | NIC                  | 192.168.1.10     | 255.255.255.0    |
| PC1         | NIC                  | 172.16.0.11      | 255.255.255.0    |
| Server      | NIC                  | 192.168.100.10   | 255.255.255.0    |

## 3. Static Routing Configuration

### Router0
```
ip route 172.16.0.0 255.255.255.0 10.0.0.2
ip route 172.16.0.0 255.255.255.0 12.0.0.2
ip route 11.0.0.0 255.255.255.252 12.0.0.2
ip route 192.168.100.0 255.255.255.0 12.0.0.2
```

### Router1
```
ip route 192.168.1.0 255.255.255.0 10.0.0.1
ip route 192.168.1.0 255.255.255.128 11.0.0.1
ip route 12.0.0.0 255.255.255.252 11.0.0.1
ip route 192.168.100.0 255.255.255.0 11.0.0.1
```

### Router2
```
ip route 192.168.1.0 255.255.255.0 12.0.0.1
ip route 172.16.0.0 255.255.255.0 11.0.0.2
ip route 0.0.0.0 0.0.0.0 11.0.0.2
```

## 4. Verification

- **Ping Results**:  
  - 192.168.1.10 ✅  
  - 172.16.0.11 ✅  
  - 192.168.100.10 ✅  

- **Show IP Route** outputs attached as screenshots.

## 5. Notes
- Project focuses on **Static Routing**.  
- Multiple routes were added for redundancy.  
- Successfully tested end-to-end connectivity.
