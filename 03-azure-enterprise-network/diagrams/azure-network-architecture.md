# Azure Enterprise Network Architecture

## Architecture Overview

This diagram documents the Azure enterprise networking lab deployed in East US.

The environment demonstrates subnet segmentation, network security groups, private connectivity, and application-level testing.

## Network Topology

```mermaid
flowchart TB
    RG["Resource Group: rg-network-engineering-lab"]

    subgraph VNET["Azure VNet: vnet-enterprise-lab | 10.20.0.0/16"]
        direction LR

        subgraph FRONT["Frontend Subnet | 10.20.1.0/24"]
            NSGF["NSG: nsg-frontend"]
            VMF["vm-frontend-test<br/>10.20.1.4<br/>Ubuntu 24.04"]
        end

        subgraph BACK["Backend Subnet | 10.20.2.0/24"]
            NSGB["NSG: nsg-backend"]
            VMB["vm-backend-test<br/>10.20.2.4<br/>Ubuntu 24.04"]
        end

        VMF -->|"TCP 8080: Allowed<br/>HTTP 200 OK"| VMB
    end

    RG --> VNET
    NSGF -.-> VMF
    NSGB -.-> VMB

    classDef network fill:#e8f2ff,stroke:#2563eb,color:#111827
    classDef security fill:#fff4df,stroke:#d97706,color:#111827
    classDef compute fill:#e7f8ed,stroke:#16a34a,color:#111827

    class RG,VNET network
    class NSGF,NSGB security
    class VMF,VMB compute
```

## Security Configuration

- Frontend and backend workloads are deployed in separate subnets.
- Network Security Groups are associated with their respective subnets.
- Backend TCP port 8080 is permitted from the frontend subnet.
- Other inbound traffic originating within the lab VNet is denied by the backend NSG.
- Neither test VM has a public IP address.

## Connectivity Validation

| Test | Result |
|---|---|
| Frontend inbound TCP 8080 | Allowed |
| Frontend external inbound SSH | Denied |
| Backend inbound TCP 8080 | Allowed |
| Backend inbound SSH | Denied |
| Frontend to backend HTTP connectivity | HTTP 200 OK |

Azure Network Watcher IP Flow Verify was used to evaluate selected security rules.

Application-level connectivity was independently validated using a Python HTTP server.

## Resource Lifecycle

Both test virtual machines were stopped and deallocated after testing to reduce Azure consumption.

The network configuration and evidence are retained for documentation and future exercises.