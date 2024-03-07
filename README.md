# aap-demo

## Links

- [AWS](https://docs.ansible.com/ansible/latest/collections/amazon/aws/docsite/aws_ec2_guide.html)
- [Azure](https://docs.ansible.com/ansible/latest/scenario_guides/guide_azure.html)
- [Chapter 12. Integrating Red Hat Satellite and Ansible Tower](https://access.redhat.com/documentation/en-us/red_hat_satellite/6.7/html/managing_hosts/chap-red_hat_satellite-managing_hosts-integrating_satellite_and_ansible_tower#doc-wrapper)


## Building EE

```sh
cd ee

# Pull the base EE
podman login registry.redhat.io
podman pull registry.redhat.io/ansible-automation-platform-24/ee-minimal-rhel8:latest

# Build the custom EE
ansible-builder build -t aap-demo-ee

# Push the EE to PAH or Container registry
podman login <REGISTRY_URL>
podman tag localhost/aap-demo-ee <REGISTRY_URL>/aap-demo-ee:v1
podman push <REGISTRY_URL>/cloud-ee:v1 --tls-verify=false
```

## Local Test

### AWS

```
# 1. Create ~/.aws/credentials
# 2. Mount the credentials and inventory in the containers
# 3. List hosts from the inventory

podman run \
  -v $HOME/.aws/credentials:/runner/.aws/credentials:Z \
  -v $PWD/inventory.aws_ec2.yml:/runner/inventory.aws_ec2.yml:Z \
  localhost/aap-demo-ee:v1  cat /runner/inventory.aws_ec2.yml

```

### GCP 

```sh
### GCP dynamic inventory
# ansible-inventory -i inventory.gcp.yml --graph
```
