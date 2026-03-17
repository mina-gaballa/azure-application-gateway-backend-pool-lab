# Azure Application Gateway Lab 🌍
Deploying and validating an Azure Application Gateway backend pool in Central India using ARM templates, PowerShell, and IIS on two backend virtual machines.

---

## 📋 Lab Overview
This lab demonstrates how to deploy backend web servers behind an **Azure Application Gateway** and validate traffic distribution and backend health in **Central India**.

The environment includes:
- 1 Virtual Network
- 1 Application Gateway
- 2 Backend Virtual Machines
- IIS installed on both VMs
- Backend health validation from Azure Portal
- Browser testing through the Application Gateway public IP

---

## 🏗️ Architecture
- 1 Virtual Network: **ContosoVNet**
- 1 Application Gateway: **ContosoAppGateway**
- 2 Backend VMs: **BackendVM1** and **BackendVM2**
- 1 Public IP attached to the Application Gateway
- 1 Backend Pool serving HTTP traffic on port 80
- IIS configured on both backend servers with customized default pages

---

## 📁 Files

| File | Description |
|------|-------------|
| `backend-centralindia.json` | ARM template to deploy the backend virtual machines and networking resources |
| `backend-centralindia.parameters.json` | Parameters file for backend deployment |
| `install-iis-centralindia.ps1` | PowerShell script to install and configure IIS on both backend VMs |

---

## 🚀 Deployment Steps

### Task 1 — Deploy Backend Resources
```powershell
$RGName = "ContosoResourceGroup"
New-AzResourceGroupDeployment -ResourceGroupName $RGName -TemplateFile backend-centralindia.json -TemplateParameterFile backend-centralindia.parameters.json
