# 🚀 Automation Hub – Centralized Azure DevOps Pipeline Templates

## 📘 Overview
**Automation Hub** is a centralized Azure DevOps pipeline repository that hosts **reusable YAML templates** for CI/CD automation.  
It provides:

- **Full pipeline templates** – ready-to-use end-to-end pipelines  
- **Modular templates** – stage-level templates that teams can pick and choose (Build, Test, Scan, Deploy, etc.)

The goal is to **standardize CI/CD practices**, **improve reuse**, and **simplify onboarding** across projects.

---

## 🎯 Key Objectives
- Promote **consistency** across all pipelines  
- Enable **reuse of proven CI/CD patterns**  
- Integrate **quality and security checks** by default  
- Support **modular pipelines** for flexible adoption  
- Maintain **single source of truth** for pipeline logic  

---

## 🧱 Recommended Repository Structure

```bash
automation-hub/
│
.azure-pipelines/
│
├── templates/
│   ├── full-pipelines/
│   │   ├── python-end-to-end.yml
│   │   ├── nodejs-end-to-end.yml
│   │   └── dotnet-end-to-end.yml
│   │
│   ├── stages/
│   │   ├── build/
│   │   │   ├── python-build.yml
│   │   │   ├── nodejs-build.yml
│   │   │   └── dotnet-build.yml
│   │   │
│   │   ├── security/
│   │   │   ├── pylint-scan.yml
│   │   │   ├── sonar-scan.yml
│   │   │   └── trivy-scan.yml
│   │   │
│   │   └── deploy/
│   │       ├── azure-functions-deploy.yml
│   │       ├── aks-deploy.yml
│   │       └── webapp-deploy.yml
│   │
│   └── modular/
│       ├── build/
│       │   ├── python-build.yml
│       │   └── nodejs-build.yml
│       │
│       ├── test/
│       │   ├── unit-test.yml
│       │   └── integration-test.yml
│       │
│       ├── scan/
│       │   ├── pylint.yml
│       │   ├── sonar.yml
│       │   └── trivy.yml
│       │
│       └── package/
│           ├── python-package.yml
│           └── nodejs-package.yml
│
└── azure-pipelines.yml       # example usage for testing / demonstration



#Tag Specific Reference (Recommended)


#Branch Specific Reference 
Reference Repository:
resources:
  repositories:
    - repository: automationHub
      type: git
      name: DevOps/automation-hub
      ref: refs/heads/main



Use Full Template:
extends:
  template: .azure-pipelines/templates/full/end-to-end.yml@automationHub
  parameters:
    environment: "dev"
    enableWizScan: true



Use Modular Template:
stages:
- template: .azure-pipelines/templates/modular/validation/pr-checks.yml@automationHub
- template: .azure-pipelines/templates/modular/build/python-build.yml@automationHub
- template: .azure-pipelines/templates/modular/test/pytest.yml@automationHub
- template: .azure-pipelines/templates/modular/deploy/webapp-deploy.yml@automationHub


