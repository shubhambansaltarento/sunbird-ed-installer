# sunbird-ed-installer

## Installing sunbird on Azure

#### Pre-requisites

1. Domain Name
2. SSL Certificate(FullChain -> private key and Certificate+CA_Bundle). **Fullchain is mandatory**, else installation will fail.

#### Required CLI tools
1. Azure CLI (https://learn.microsoft.com/en-us/cli/azure/install-azure-cli)
2. jq (https://jqlang.github.io/jq/download/)
3. rclone (https://rclone.org/)
4. Terraform (https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli)
5. Terragrunt (https://terragrunt.gruntwork.io/docs/getting-started/install/)
7. Linux / Macos / Gitbash (Windows)
8. Python 3
9. PyJwt python package (you can using using pip)
10. [kubectl](https://kubernetes.io/docs/tasks/tools/)
11. [helm](https://helm.sh/docs/intro/quickstart/#install-helm)

**Note:**

We will copy your existing files in the below location with a `.bak` extension and create overwrite the below files
- `~/.config/rclone/rclone.conf`
- `~/.kube/config`

- In the below instructions `demo` is the environement name. You can change it as per your need. For example - `dev`, `stage` etc.
- Clone the repo
`git cline git@github.com:nimbushubin/sunbird.git`
- Copy the template directory `cd terraform/azure && cp -r template demo`
- Fill the variables in `demo/env.hcl`
- Fill the variables in `demo/global-values.yaml`
- Run `az login --tenant AZURE_TENANT_ID`
- Run `time ./install.sh`

#### Mandatory variables in `env.hcl`
|      Name      |   Description    |
|----------------|------------------|
|`environment`   | Environment name (between 1 - 9 charcaters). Example: *dev*, *stage* |
|`random_string` | Alphanumeric random string (between 12 - 24) characters. Example: *U2PNfwcz6rb9756ZwAwZ*  |

#### Mandatory variables in `global-values.yaml`
|      Name      |   Description   |
|----------------|-----------------|
|`domain`           | Domain name  |
|`proxy_private_key` | SSL private key |
|`proxy_certificate` | SSL public key |

## Installation Steps

1. Create environment folder

```bash
cd terraform/<cloud>
cp -rf template dev
cd dev
```
2. Update required values in `environment.hcl` and `global-values.yaml` files
3. Run `bash install.sh`