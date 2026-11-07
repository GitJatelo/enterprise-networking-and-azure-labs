# Azure Enterprise Networking & Network Security Lab

## Project Overview

Designed, deployed, and validated a segmented enterprise-style network
in Microsoft Azure using private virtual machines, Network Security
Groups (NSGs), and Azure Network Watcher.

This hands-on lab demonstrates Azure networking, subnet segmentation,
traffic filtering, connectivity troubleshooting, and cost management.

## Technologies

- Microsoft Azure
- Azure Virtual Network (VNet)
- Azure Network Security Groups (NSGs)
- Azure Network Watcher
- Azure Virtual Machines
- Ubuntu Server 24.04 LTS
- Azure Cost Management
- Linux, TCP/IP, HTTP, SSH

## Network Architecture

| Component | Configuration |
|---|---|
| Resource Group | rg-network-engineering-lab |
| Azure Region | East US |
| Virtual Network | vnet-enterprise-lab |
| VNet Address Space | 10.20.0.0/16 |
| Frontend Subnet | Snet-Frontend â€” 10.20.1.0/24 |
| Backend Subnet | Snet-Backend â€” 10.20.2.0/24 |
| Frontend VM | vm-frontend-test â€” 10.20.1.4 |
| Backend VM | vm-backend-test â€” 10.20.2.4 |
| Operating System | Ubuntu Server 24.04 |
| VM Size | Standard D2ds v4 |
| Public IP Addresses | None |

## Network Security Configuration

Two Network Security Groups were configured:

- nsg-frontend
- nsg-backend

### Backend Security Rules

| Priority | Rule | Action |
|---|---|---|
| 100 | Allow-Frontend-To-Backend-8080 | Allow TCP 8080 |
| 200 | Deny-VNet-To-Backend | Deny other traffic from 10.20.0.0/16 |

The allow rule permits TCP 8080 traffic from the frontend subnet
(10.20.1.0/24) to the backend subnet (10.20.2.0/24).

The deny rule blocks other traffic originating within the lab VNet
address space from reaching the backend subnet.

## Security Validation

Azure Network Watcher IP Flow Verify was used to evaluate NSG decisions.

### Test 1 â€” Frontend to Backend TCP 8080

Source: 10.20.1.4
Destination: 10.20.2.4
Destination Port: 8080

Result: ALLOWED

Matching rule: Allow-Frontend-To-Backend-8080

### Test 2 â€” Frontend to Backend SSH

Source: 10.20.1.4
Destination: 10.20.2.4
Destination Port: 22

Result: DENIED

Matching rule: Deny-VNet-To-Backend

### Test 3 â€” External SSH to Frontend

Simulated source: 8.8.8.8
Destination: 10.20.1.4
Destination Port: 22

Result: DENIED

Matching rule: DenyAllInBound

## End-to-End Connectivity Validation

A Python HTTP server was started on the backend VM using TCP port 8080.

The frontend VM initiated an HTTP request to:

http://10.20.2.4:8080

The request returned:

HTTP/1.0 200 OK

The response confirmed successful application-layer communication
between the frontend and backend virtual machines.

This test demonstrates actual connectivity in addition to NSG
rule evaluation.

## Cost Management

The lab uses an Azure for Students subscription.

Cost-management measures include:

- A $10 monthly budget with alerts at 50%, 80%, and 100%
- Private VMs without public IP addresses
- Scheduled VM auto-shutdown
- Deallocation of both test VMs after validation

Budget alerts provide notifications but do not enforce a spending cap.

## Evidence

Deployment, security, connectivity, and cost-management evidence
is maintained in the screenshots directory.

Screenshots are reviewed for sensitive subscription and account
information before publication.

## Project Status

Completed and verified:

- Virtual network and subnet deployment
- NSG creation and subnet associations
- Custom inbound security rules
- Frontend and backend VM deployment
- Azure Network Watcher IP Flow Verify tests
- Successful frontend-to-backend HTTP connectivity
- VM deallocation after testing

## Skills Demonstrated

Azure Networking | Network Segmentation | NSG Configuration |
TCP/IP | Network Troubleshooting | Cloud Security |
Linux Administration | Azure Cost Management
