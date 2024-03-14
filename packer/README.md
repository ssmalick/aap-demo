# Build Images with packer


## Steps

- Get aws credentials and setup env variables on the management host
- Install packer and aws plugin
- Use the [AWS template](https://developer.hashicorp.com/packer/tutorials/aws-get-started/aws-get-started-build-image) provided by hashicorp
- Validate and build the template
- Verify by visiting the AWS AMI page 
- [Optional] Check if packer saves state by reruning the build

- Create AAP execution environment including packer
- Create a playbook to automate the build
- Create AAP job with related resources
- Test 


## Packer Installation

1. Download the binary
2. Extract it and move it to the PATH
3. Install packer aws plugin

```sh
packer plugins install github.com/hashicorp/amazon
```

## Building the image

- [Build EC2 AMI](https://developer.hashicorp.com/packer/tutorials/aws-get-started/aws-get-started-build-image)


```sh
### Initialize packer configuration
packer init .

### Format and validate the template
packer fmt .
packer validate .

### Build the image
packer build aws-ubuntu.pkr.hcl
```

Visit AWS AMI page to verify

## Build AAP EE

```sh
cd ee/packer
ansible-builder build -t packer

# tag and push image to hub
```

## Alternative

- Check if image build is provided by AWS collection
