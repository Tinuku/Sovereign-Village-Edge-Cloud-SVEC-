# Sovereign Village Edge Cloud (SVEC)
### Infrastructure-as-Code (IaC) for Resilient Distributed Systems

## Overview
SVEC is a private-cloud infrastructure project designed for deterministic control of edge-computing nodes. By leveraging Proxmox VE as a hypervisor and Terraform as the orchestration layer, the system abstracts heterogeneous hardware into a unified, programmable data plane.

## Design Objectives
* **Sovereignty:** Zero-dependency on public cloud providers for core logic.
* **Auditability:** Full version control of infrastructure state via GitOps.
* **Security:** Hardened Zero-Trust networking via Wireguard-encapsulated management traffic.

## Architecture Specification
The system utilizes a decoupled Control Plane architecture to manage geographically distributed nodes.

```mermaid
graph LR
    subgraph Management_Layer
        TF[Terraform/OpenTofu]
        AN[Ansible]
    end

    subgraph Transport
        WG((Wireguard Tunnel))
    end

    subgraph Execution_Layer
        PVE[Proxmox Cluster]
        LXC[Telemetry Containers]
        KVM[Compute Nodes]
    end

    TF --> WG --> PVE
    PVE --> LXC
    PVE --> KVM
