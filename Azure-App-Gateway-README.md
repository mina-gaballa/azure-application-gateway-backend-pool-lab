# Azure Application Gateway Lab 🌍
Deploying and validating an Azure Application Gateway backend pool in Central India using ARM templates, PowerShell, and IIS on two backend virtual machines.

---

## 📋 Lab Overview
This lab demonstrates how to deploy backend web servers behind an Azure Application Gateway and validate traffic distribution and backend health in Central India.

### The environment includes:
- 1 Virtual Network
- 1 Application Gateway
- 2 Backend Virtual Machines
- IIS installed on both VMs
- Backend health validation from Azure Portal
- Browser testing through the Application Gateway public IP

---

## 🏗️ Architecture
- 1 Virtual Network: ContosoVNet
- 1 Application Gateway: ContosoAppGateway
- 2 Backend VMs: BackendVM1 and BackendVM2
- 1 Public IP attached to the Application Gateway
- 1 Backend Pool serving HTTP traffic on port 80
- IIS configured on both backend servers with customized default pages

---

## 📁 Files

| File | Description |
|------|-------------|
| backend-centralindia.json | ARM template to deploy the backend virtual machines and networking resources |
| backend-centralindia.parameters.json | Parameters file for backend deployment |
| install-iis-centralindia.ps1 | PowerShell script to install and configure IIS on both backend VMs |

---

## 🚀 Deployment Steps

### Task 1 — Deploy Backend Resources
```powershell
$RGName = "ContosoResourceGroup"
New-AzResourceGroupDeployment -ResourceGroupName $RGName -TemplateFile backend-centralindia.json -TemplateParameterFile backend-centralindia.parameters.json
```

This deployment creates:
- BackendVM1
- BackendVM2
- Network interfaces for both VMs
- Supporting resources in Central India

---

### Task 2 — Install IIS on BackendVM1
```powershell
Invoke-AzVMRunCommand -ResourceGroupName 'ContosoResourceGroup' -Name 'BackendVM1' -CommandId 'RunPowerShellScript' -ScriptPath 'install-iis-centralindia.ps1'
```

---

### Task 3 — Install IIS on BackendVM2
```powershell
Invoke-AzVMRunCommand -ResourceGroupName 'ContosoResourceGroup' -Name 'BackendVM2' -CommandId 'RunPowerShellScript' -ScriptPath 'install-iis-centralindia.ps1'
```

The script installs IIS and customizes the default page so each server displays its own VM name.

---

### Task 4 — Validate Backend Health

In Azure Portal:
- Open ContosoAppGateway
- Go to Backend health
- Confirm both backend servers are marked Healthy
- Verify that the probe receives HTTP 200 status code

Expected healthy backend IPs:
- 10.0.1.4
- 10.0.1.5

---

### Task 5 — Test Through the Application Gateway Public IP

Open the Application Gateway public IP in the browser:
```
http://20.219.244.30
```

Refresh multiple times to confirm responses from:
- BackendVM1
- BackendVM2

This verifies that the Application Gateway is successfully routing traffic to both backend servers.

---

## 📸 Screenshots
- All Resources
- Application Gateway Backend Health
- Browser Test — BackendVM1
- Browser Test — BackendVM2

---

## ✅ Validation Results
- Both backend VMs deployed successfully
- IIS installed and running on both servers
- Azure Application Gateway backend health shows both servers as Healthy
- Health probe returned 200 OK
- Browser testing confirmed successful routing to both backend servers

---

## 🔧 Technologies Used
- Azure Application Gateway
- Azure Virtual Network
- Azure Virtual Machines
- ARM Templates
- PowerShell (Az Module)
- IIS

---

## 👤 Author
Mina Gaballa
