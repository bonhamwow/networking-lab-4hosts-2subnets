# networking-lab-4hosts-2subnets
## Obective:
In this lab, I build and configure a network topology consisting of **4 hosts divided equally across 2 distinct subnets**, connected via a router (or layer 3 device).
```mermaid
graph TD
    subgraph SubnetA["Subnet A: 192.168.10.0/24"]
        direction TB
        HostA1["<b>host-a1</b><br/>IP: 192.168.10.2/24<br/>GW: 192.168.10.1"]
        HostA2["<b>host-a2</b><br/>IP: 192.168.10.3/24<br/>GW: 192.168.10.1"]
        SwitchA["<b>switch-a</b><br/>Linux Bridge: br0"]
        
        HostA1 -- "eth1 ↔ eth1" --> SwitchA
        HostA2 -- "eth1 ↔ eth2" --> SwitchA
    end

    Router["<b>router</b><br/>FRRouting / Linux Router<br/>eth1: 192.168.10.1/24<br/>eth2: 192.168.20.1/24"]

    subgraph SubnetB["Subnet B: 192.168.20.0/24"]
        direction TB
        SwitchB["<b>switch-b</b><br/>Linux Bridge: br0"]
        HostB1["<b>host-b1</b><br/>IP: 192.168.20.2/24<br/>GW: 192.168.20.1"]
        HostB2["<b>host-b2</b><br/>IP: 192.168.20.3/24<br/>GW: 192.168.20.1"]
        
        SwitchB -- "eth1 ↔ eth1" --> HostB1
        SwitchB -- "eth2 ↔ eth1" --> HostB2
    end

    SwitchA -- "eth3 ↔ eth1" --> Router
    Router -- "eth2 ↔ eth3" --> SwitchB

    classDef host fill:#e1f5fe,stroke:#0288d1,stroke-width:2px,color:#01579b;
    classDef switch fill:#fff3e0,stroke:#f57c00,stroke-width:2px,color:#e65100;
    classDef router fill:#e8f5e9,stroke:#388e3c,stroke-width:2px,color:#1b5e20;
    
    class HostA1,HostA2,HostB1,HostB2 host;
    class SwitchA,SwitchB switch;
    class Router router;
```

