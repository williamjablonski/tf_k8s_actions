# Soft # Automate Kubernetes Deployment using Terraform and Github Actions


## Softdesign TASK 1
Terraform code that will create a namespace and deploys the Nginx server in the minikube cluster and TF code verification and deployment has been automated using GitHub actions

## How I built
- Created a GitHub Actions workflow using the Marketplace Github actions plugins,
    - `actions/checkout@v2.5.0` -> to Checkout the code
    - `medyagh/setup-minikube@v0.0.13` -> to setup `minikube`
    - `Azure/setup-kubectl@v3` -> to setup `kubectl`
    - `hashicorp/setup-terraform@v2.0.2` -> to setup `terraform`
- This workflow can be used in development environments, in which an Infra developer can create the Terraform code to deploy kubernetes workload. Once after creating the tf code, the developer can trigger the Terraform workflow, that will do the CI for Terraform code, and deploy the infra in `minikube`.
- The kube config context has been created as a variable in Terraform, so it can be overridden with other Kubernetes Cluster config and contexts from Cloud providers like Amazon EKS or Azure AKS or GCP GKE Clusters.

### Triggering the Workflow
This workflow can be triggered from the `actions` tab, by providing the Terraform code directory as an input.
So it will run the below steps in the directory provided as input,
1. Workflow installs, `minikube`, `kubectl` and `terraform` CLI executables needed to be used by the rest of workflow
2. It runs `terraform init` command to download the `kubernetes` provider
3. Then runs `terraform validate` command to check the tf code is valid or not
4. After that it runs, `terraform plan` and `terraform apply`  commands and performs the Kubernetes namespace creation and deploys the nginx server. 
5. Workflow also has `terraform destroy` command, that deletes the kubernetes infra created in the workflow

### Documentation / guide
- [Terraform Kubernetes Provider](https://registry.terraform.io/providers/hashicorp/kubernetes/latest/docs)
- [Workflow Dispatch Inputs](https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions#onworkflow_dispatchinputs)
- [Jobs](https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions#jobs)
- [Terraform Market place Action](https://github.com/marketplace/actions/hashicorp-setup-terraform)

### Helper
https://medium.com/@yogitakothadia/a-manifest-file-in-kubernetes-952183a508d4

## Execution Log

Pipeline
![alt text](http://url/to/img.png)

Log
![alt text](http://url/to/img.png)
