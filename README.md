# Demo presentation - TMCSP-PT

Demo: **Kubernetes cluster in 10 minutes** using the tools

- [Hashicorp Vagrant](https://www.vagrantup.com/) to spin up a Terraform + Ansible VirtualBox
- [Hashicorp Terraform](https://www.terraform.io/) to create Infrastructure in the Cloud
- [Red Hat Ansible](https://www.ansible.com/) to automate installation of K8s cluster

## Create a VirtualBox VM with Vagrant

We create a local VM with Terraform and Ansible installed.

    vagrant up

Open a shell to the VM.

    vagrant ssh

The current directory is shared inside the VM on `/vagrant`.

    cd /vagrant

Before continuing with the deployment in the next section, 
setup your `~/.aws/credentials`
and your `private SSH key`.

## Create Infrastructure in AWS Cloud with Terraform

Set the name of your EC2 key pair name

- for Windows PowerShell:

        $env:TF_VAR_ssh_key = "key_name"

- for Linux/MacOS:

        export TF_VAR_ssh_key="key_name"

Apply Terraform

```
cd terraform
terraform init
terraform apply -auto-approve
```

This will create EC2 instances and write their public ip addresses into the file `ansible/inventory`.

## Provision Kubernetes Cluster with Ansible

Run the Ansible Playbook

```
cd ..
cd ansible
ansible-galaxy install -r roles/requirements.yml
ansible-playbook -i inventory main.yml
```

## Kubernetes Example deployment

    kubectl apply -f https://github.com/thomasstxyz/fhb-mcce-ineni-pt-iac-demo/blob/main/kubernetes/manifests/podtato-kubectl.yaml

# License

MIT

# Author Information

This project was created in 2022 by [Thomas Stadler](https://github.com/thomasstxyz).
