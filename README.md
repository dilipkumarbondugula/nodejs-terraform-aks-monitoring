# 🚀 Azure AKS CI/CD Automation Project

This project sets up a fully automated CI/CD pipeline using:

- **Azure Kubernetes Service (AKS)**
- **Azure Container Registry (ACR)**
- **Terraform** (for infrastructure)
- **Azure DevOps** (CI/CD pipelines)
- **GitHub** (source control)
- **Prometheus + Grafana** (monitoring via Helm)

---

## 📦 Project Structure

```
azure-aks-automation/
├── app/                      # Node.js application
├── terraform/                # AKS + ACR provisioning scripts
├── manifests/                # Kubernetes manifests
├── helm/                     # Monitoring installation scripts
└── .azure-pipelines/         # Azure DevOps pipeline YAML
```

---

## 🚧 Prerequisites

- Azure account with at least **$50 credits**
- Azure DevOps account
- GitHub repository (connect it to Azure DevOps)
- Azure DevOps Service Connection to your Azure subscription

---

## 🔧 Setup Instructions

### 1. Clone and Push to GitHub

```bash
git clone <this-repo-url>
cd azure-aks-automation
```

Push this code to your GitHub repo.

---

### 2. Configure Azure DevOps Pipeline

- Create a new project in Azure DevOps
- Go to **Pipelines → New Pipeline**
- Choose **GitHub (YAML)** and select your repo
- It should auto-detect `.azure-pipelines/azure-pipelines.yml`

> Make sure you have created a **Service Connection** in Azure DevOps:
> - Go to **Project Settings → Service connections**
> - Create a new one for Azure Resource Manager (using service principal)
> - Name it exactly as referenced in the YAML (`<Your Azure DevOps Service Connection>`)

---

### 3. Let the Pipeline Run

On push to the `main` branch, this will:
1. Provision Azure resources via **Terraform**
2. Build and push Docker image to ACR
3. Deploy app to AKS
4. Install **Prometheus + Grafana** via Helm

---

## 🌐 Access Your App

- Use `kubectl get svc` to retrieve the **external IP**
- Visit it in your browser to see `Hello from AKS!`

---

## 📊 Access Monitoring

- Use `kubectl get svc -n monitoring` to get Grafana's LoadBalancer IP
- Default credentials:
  - **Username:** admin
  - **Password:** prom-operator

---

## 📌 Notes

- ACR name must be globally unique; modify if necessary in `terraform/main.tf`
- You can manage cost by deleting the resource group after use:

```bash
az group delete --name aks-rg --yes --no-wait
```

---

## 🙌 Credits

Created using:
- [Terraform](https://www.terraform.io/)
- [Azure AKS](https://azure.microsoft.com/en-us/products/kubernetes-service/)
- [Helm](https://helm.sh/)
- [Prometheus Operator](https://github.com/prometheus-operator/kube-prometheus)

---

Happy DevOps-ing! 🚀
