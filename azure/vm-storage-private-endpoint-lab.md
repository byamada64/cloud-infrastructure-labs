# ☁️ Azure VM + Storage + Container + Private Endpoint Lab

## 🎯 Objective

Provisioned a repeatable multi-service Azure environment to validate compute deployment, secure storage access, private networking, governance tagging, container workloads, remote administration, and lifecycle cleanup awareness.

---

## 🏗️ Environment Build Choices

### 🏷️ Resource Group / Networking

- **Resource Group:** Existing lab resource group reused
- **Virtual Network:** Default Azure lab VNet used
- **Subnet:** Default subnet selected
- **Public IP:** Enabled temporarily for testing
- **Purpose:** Fast lab deployment with minimal custom networking
- **Enterprise Note:** Production environments may require dedicated VNets, subnet planning, NSGs, routing controls, private DNS, firewall review, and formal network requests.

### 🖥️ VM

- **VM Name:** `az-lab-vm`
- **Region:** East US
- **Availability Zone:** Zone-aware deployment enabled
- **Operating System:** Windows Server Datacenter (2022 / 2025 lab image)
- **VM Size:** Standard D2s_v3
- **Security Type:** Trusted Launch
- **Secure Boot:** Enabled
- **vTPM:** Enabled
- **Public RDP Access:** Enabled temporarily for testing
- **Access Method:** Microsoft Remote Desktop from macOS
- **Purpose:** Administrative access and validation testing

### 📦 Storage

- **Storage Account Name:** `bypepstorage01`
- **Region:** East US
- **Performance Tier:** Standard
- **Account Type:** GPv2
- **Redundancy:** LRS
- **Blob Services:** Enabled
- **Public Access:** Enabled during initial testing
- **Purpose:** Blob storage, SAS testing, private connectivity

### 🗂️ Blob Container

- **Container Type:** Blob container
- **Validation File:** `index_01.html`
- **Access Method:** SAS URL generated for controlled temporary access
- **Purpose:** Static file validation and object access testing

### 🐳 Containers

- **Deployment Type:** Azure Container Instance
- **Container Name:** `by-nginx01`
- **Image Source:** Quickstart Images
- **Image Used:** `nginx`
- **Region:** East US
- **CPU:** 1 vCPU
- **Memory:** 1.5 GB
- **Public Endpoint:** Enabled
- **Port:** 80
- **Purpose:** Lightweight web workload validation

### 🔒 Private Endpoint (PEP)

- **Resource Type:** Storage Account
- **Target Resource:** `bypepstorage01`
- **Subresource:** `blob`
- **Region:** East US
- **Purpose:** Private network path to Blob Storage

### 🏷️ Governance / Enterprise Awareness

- Applied **Tags** for:
  - Accounting
  - Billing
  - Ownership
  - Environment
  - Lifecycle / Lab Use
- Reused existing Resource Group
- Cost-aware sizing used where possible
- Demonstrates enterprise resource management practices

---

## 💻 Commands Used

### 🖥️ VM / Azure CLI

- `az vm create`
- `az vm show`
- `az vm list`
- `az vm open-port --port 3389`

### 📦 Storage / Azure CLI

- `az storage account create`
- `az storage account list`
- `az storage container create`
- `az storage blob upload`
- `az storage blob list`

### 🔑 SAS / Blob Access

- `az storage blob generate-sas`
- `az storage blob url`

### 🐳 Containers

- `az container create`
- `az container show`
- `az container list`
- `az container logs`

### 🔒 Private Endpoint (PEP)

- `az network private-endpoint create`
- `az network private-endpoint list`
- `az network private-dns zone list`

### 🖥️ Windows CMD Validation (Inside VM)

- `nslookup <storage-account-name>.blob.core.windows.net`
- `ping <target-host>` *(if allowed)*
- `ipconfig`
- `hostname`

### 🧹 Cleanup

- `az resource list --resource-group <resource-group-name>`
- `az vm delete`
- `az container delete`
- `az group delete`
