# Example Packer configuration files for building Ubuntu 18.04 Server Image for VMware ESXi 6.7 platform

All examples were run on an ubuntu 18.04 virtual machine

Packer version 1.5.6 was used as the brew install of Packer at the time of writing.

Originally forked from https://github.com/allthingsclowd/packer-vsphere-iso-example

## Prerequisite to running the build process:

- Clone this repository

``` bash
git clone https://github.com/sdorsett/packer-vsphere-ubuntu-1804.git 
```

- Configure the `.variables` file

``` bash
{
    "vcenter_server":"YOUR VCENTER IP ADDRESS",
    "username":"administrator@vsphere.local",
    "password":"VCENTER PASSWORD",
    "datastore":"datastore1",
    "host":"ESXi IP ADDRESS",
    "cluster": "CLUSTER NAME",
    "network": "VM Network",
    "resource_pool": "",
    "ssh_username": "ubuntu",
    "ssh_password": "my_secret_password",
    "ssh_key_src_pub": "id_rsa.pub",
    "image_home_dir": "/home/"
}
```

- Copy your public ssh key that you'll use to access the VM remotely to the packer directory and call it `id_rsa.pub`

- Download the ubuntu server .iso and upload it to the datastore location that is described in packer/server.json 

``` json
        "iso_paths": [
          "[datastore_name] isos/ubuntu-18.04.3-server-amd64.iso"
        ],
```

- Change into the packer directory

``` bash
cd packer
```

- Download [packer version 1.5.6](https://releases.hashicorp.com/packer/1.5.6/packer_1.5.6_linux_amd64.zip)

```bash
wget https://releases.hashicorp.com/packer/1.5.6/packer_1.5.6_linux_amd64.zip
unzip packer_1.5.6_darwin_amd64.zip
chmod +x packer
```

## Example command used to build a server image template

``` bash
./packer build -force -var-file=../.variables server.json
```
