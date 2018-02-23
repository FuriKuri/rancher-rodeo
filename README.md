# rancher-rodeo

# Vagrant users
* https://www.vagrantup.com/ (For installing Vagrant)
* https://www.mls-software.com/opensshd.html (Windows only, install OpenSSHD on Windows to ensure vagrant can ssh into nodes to do provisioning
* Get started with:
```
$ git clone https://github.com/furikuri/rancher-rodeo && cd rancher-rodeo
$ vagrant up
$ vagrant ssh rancherserver
```

# AWS users
* https://docs.aws.amazon.com/cli/latest/userguide/installing.html (For installing AWS CLI)
* Get started with:
```
$ git clone https://github.com/furikuri/rancher-rodeo && cd rancher-rodeo
$ publickey=$(cat ~/.ssh/id_rsa.pub)
$ publiccidrblock="$(dig +short myip.opendns.com @resolver1.opendns.com)/32"
$ aws cloudformation create-stack --capabilities CAPABILITY_IAM --stack-name rancher-instances --template-body file://cloudformation/rancher.yaml --parameters ParameterKey=SSHPublicKey,ParameterValue=$publickey ParameterKey=AllowedCidrBlock,ParameterValue=$publiccidrblock

# Get all public ips
$ aws ec2 describe-instances --filters Name=tag-key,Values=Rancher | jq '.Reservations[].Instances[].PublicIpAddress'

# SSH into rancher instance
$ ssh rancher@<ip>
```

# Running Rancher
* `sudo docker run -d -p 8080:8080 rancher/server`