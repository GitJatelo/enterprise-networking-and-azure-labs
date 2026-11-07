# Enterprise Networking and Azure Labs

**Enterprise Network Engineering | Microsoft Azure | Network Security | Troubleshooting**

## Project Overview

A hands-on networking portfolio demonstrating enterprise network architecture, Azure virtual networking, network segmentation, security controls, and connectivity troubleshooting.

The repository documents practical exercises and verified implementations designed to develop cloud infrastructure and network engineering skills.

## Repository Structure

### 01 — Enterprise Network

Enterprise networking configurations, network topology exercises, and supporting documentation.

**Focus areas:**

* IP addressing and subnetting
* Routing and switching
* VLANs and network segmentation
* Network security fundamentals

### 02 — Network Diagnostics

Network troubleshooting exercises, diagnostic evidence, packet captures, and incident documentation.

**Focus areas:**

* TCP/IP connectivity troubleshooting
* Network traffic analysis
* Packet inspection
* Incident documentation

### 03 — Azure Enterprise Network

A hands-on Azure networking implementation using an Azure for Students subscription.

### Network Architecture Diagram

Explore the Azure network topology, subnet segmentation, network security groups, and validated private connectivity.

[View Azure Enterprise Network Architecture](03-azure-enterprise-network/diagrams/azure-network-architecture.md)

**Implemented architecture:**

| Component           | Configuration              |
| ------------------- | -------------------------- |
| Azure region        | East US                    |
| Resource group      | rg-network-engineering-lab |
| Virtual network     | vnet-enterprise-lab        |
| VNet address space  | 10.20.0.0/16               |
| Frontend subnet     | 10.20.1.0/24               |
| Backend subnet      | 10.20.2.0/24               |
| Frontend VM         | vm-frontend-test           |
| Backend VM          | vm-backend-test            |
| Frontend private IP | 10.20.1.4                  |
| Backend private IP  | 10.20.2.4                  |
| Network security    | Subnet-level NSGs          |
| Operating system    | Ubuntu Server 24.04 LTS    |

## Security Implementation

Implemented subnet-level network security groups to control traffic between frontend and backend workloads.

Configured backend security rules to:

* Allow TCP port 8080 from the frontend subnet.
* Deny other inbound traffic originating from the lab VNet to the backend subnet.

Both test virtual machines were deployed without public IP addresses.

## Connectivity Validation

Verified network security rules using Azure Network Watcher IP Flow Verify.

**Successful tests:**

* Frontend-to-backend TCP port 8080: Allowed
* Frontend-to-backend TCP port 22: Denied
* External inbound SSH to frontend: Denied

Performed an additional application-level connectivity test using a Python HTTP server on the backend VM.

The frontend VM successfully connected to the backend service over TCP port 8080 and received an HTTP 200 response.

## Cost Management

Implemented cost-conscious lab practices, including:

* Azure for Students subscription
* Monthly budget and spending alerts
* Manual VM deallocation after testing
* Avoidance of unnecessary public IP addresses

Both test VMs were confirmed stopped and deallocated following connectivity testing.

## Technical Validation and Evidence

The Azure networking lab includes 30 documented screenshots covering resource deployment, network security configuration, connectivity validation, and cost management.

### Network Architecture

The environment consists of one Azure Virtual Network (`10.20.0.0/16`) divided into two application subnets:

| Network Component | Address |
|---|---|
| Frontend subnet | 10.20.1.0/24 |
| Backend subnet | 10.20.2.0/24 |
| Frontend test VM | 10.20.1.4 |
| Backend test VM | 10.20.2.4 |

Both virtual machines were deployed without public IP addresses.

### Network Security Validation

Azure Network Watcher IP Flow Verify was used to evaluate traffic against the configured Network Security Group rules.

| Test | Result | Evidence |
|---|---|---|
| Frontend inbound TCP 8080 | Allowed | [Screenshot 21](03-azure-enterprise-network/screenshots/21-frontend-inbound-8080-allowed.png) |
| Frontend external SSH | Denied | [Screenshot 22](03-azure-enterprise-network/screenshots/22-frontend-external-ssh-denied.png) |
| Backend inbound TCP 8080 | Allowed | [Screenshot 25](03-azure-enterprise-network/screenshots/25-backend-inbound-8080-allowed.png) |
| Backend inbound SSH | Denied | [Screenshot 26](03-azure-enterprise-network/screenshots/26-backend-inbound-ssh-denied.png) |

These tests document the evaluated source, destination, protocol, and port combinations. They do not constitute exhaustive testing of all possible network paths.

### Application Connectivity Testing

A Python HTTP server was started on the backend VM, listening on TCP port 8080.

The frontend VM successfully accessed the backend service using its private IP address.

**Result:** HTTP 200 OK.

Evidence:

- [Backend HTTP server](03-azure-enterprise-network/screenshots/27-backend-http-server-running.png)
- [Successful frontend-to-backend connectivity](03-azure-enterprise-network/screenshots/28-frontend-to-backend-http-success.png)

### Cost Management and Resource Lifecycle

The lab includes Azure budget monitoring and resource lifecycle controls.

- Monthly Azure budget configured with spending alerts.
- Temporary virtual machines used for connectivity testing.
- Both test VMs stopped and deallocated after validation.

Evidence:

- [Azure budget and alerts](03-azure-enterprise-network/screenshots/15-azure-budget-and-alerts.png)
- [Frontend VM deallocated](03-azure-enterprise-network/screenshots/29-frontend-vm-deallocated.png)
- [Backend VM deallocated](03-azure-enterprise-network/screenshots/30-backend-vm-deallocated.png)

**Note:** Azure budget alerts provide spending notifications but do not automatically stop resources or enforce a hard spending limit.


## Technologies

Microsoft Azure | Azure Virtual Network | Network Security Groups | Azure Network Watcher | Linux | TCP/IP | HTTP | PowerShell | Git | GitHub

## Project Status

**Azure networking deployment and initial connectivity validation completed.**

Additional architecture documentation, diagnostics, and evidence organization are in progress.

## Portfolio Purpose

This repository demonstrates practical skills relevant to:

* Azure Administrator
* Cloud Support Engineer
* Network Engineer
* Infrastructure Support Engineer
* Cloud Infrastructure Engineer

All environments use synthetic lab configurations and test workloads.
