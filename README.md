# UCN Sandbox Topologies

Welcome to the **UCN Sandbox Topologies** repository. This project contains Infrastructure as Code (IaC) and network simulation environments for Arista data center fabrics. It leverages **Containerlab** to spin up virtual cEOS routers and **Arista Validated Designs (AVD)** to build, deploy, and validate the network configurations.

## 🏗️ Topologies Included

This repository contains two primary data center designs:
1. **`l2ls_dc`**: Layer 2 Leaf-Spine Architecture.
2. **`l3ls_dc`**: Layer 3 Leaf-Spine Architecture (BGP EVPN/VXLAN).

Each topology directory is self-contained with its own Containerlab topology (`clab/`) and Arista AVD automation code (`avd/`).

## 📂 Repository Structure

The structure for both topologies follows a standard pattern. Here is the layout for `l3ls_dc`:

```text
l3ls_dc/
├── Makefile                 # Shortcut commands for Lab and AVD operations
├── clab/                    # Containerlab definition and startup configs
│   └── topology.clab.yml    # The virtual topology file
└── avd/                     # Arista AVD Automation Directory
    ├── group_vars/          # YAML variables defining the fabric and node types
    ├── inventory.yml        # Ansible inventory mapping nodes to groups
    ├── playbooks/           # Ansible playbooks (build, deploy, validate)
    ├── intended/            # Auto-generated structured configs and EOS CLI configs
    ├── documentation/       # Auto-generated fabric and device documentation
    └── anta/                # Network validation catalogs and reports
```

## 🚀 Getting Started

### 1. Clone the Repository
To get started, clone the repository to your local automation host:
```bash
git clone https://github.com/hazardsg/ucn_sandbox_topos.git
cd ucn_sandbox_topos
```

### 2. Prerequisites
To run these labs locally, you will need the following installed on your machine:
* [Docker](https://docs.docker.com/get-docker/)
* [Containerlab](https://containerlab.dev/install/)
* Python 3.x and Ansible Core
* [Arista AVD Collection](https://avd.arista.com/6.0/docs/installation/collection-installation.html) (`ansible-galaxy collection install arista.avd`)
* Arista cEOS image imported into Docker (e.g., `ceos:latest`)

### 3. Start the Virtual Lab
Navigate to the topology you want to work on (e.g., `cd l3ls_dc`) and use the `Makefile` to spin up the Containerlab environment:
```bash
make start
```
To view the status, hostnames, and management IP addresses of your deployed containers, run:
```bash
make inspect
```
*Note: You can connect to a lab device via SSH using `ssh admin@<hostname>` with the password `admin`.*

### 4. Build the Network Configurations
Once the variables in `avd/group_vars/` are defined, generate the Arista EOS configurations and the markdown documentation:
```bash
make build
```
*This parses your data models and populates the `avd/intended/` and `avd/documentation/` directories.*

### 5. Deploy the Configurations
Push the generated configurations directly to the cEOS containers running in Containerlab via eAPI:
```bash
make deploy
```

### 6. Validate the Fabric
After deployment, run the ANTA (Arista Network Test Automation) framework to verify the health, reachability, and state of your network:
```bash
make validate
```
*Validation reports are saved as CSV, JSON, and Markdown in `avd/anta/reports/`.*

### 🛑 Tearing Down the Lab
When you are finished testing, cleanly destroy the Containerlab environment and free up resources:
```bash
make stop
```
