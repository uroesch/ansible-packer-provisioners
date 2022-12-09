# packer-provisioning

This Ansible playbook and role is meant to be used from within packer.

## Sample HCL packer code

### Base provisioning 

* Installs `hyper-v` and `vmware` kernel modules and recreates `vmlinux` images. 
* Installs required repos.
* Installs and setups `cloud-init`. 

```hcl
provisioner "ansible" {
  only            = [ "qemu.base" ]
  playbook_file   = "./provisioners/postinstall.yml"
  extra_arguments = [ "--diff" ]
  max_retries     = 30
}
```

### VMware provisioning 

* Install `open-vm-tools` and `perl`.

```hcl
provisioner "ansible" {
  only            = [ "qemu.vmware" ]
  playbook_file   = "./provisioners/postinstall.yml"
  extra_arguments = [ "--diff", "--tags", "vmware" ]
}
```

### Azure provisioning 

* Install `hyper-v` daemons.
* Special `cloud-init` cleanup tasks.

```hcl
provisioner "ansible" {
  only            = [ "qemu.azure" ]
  playbook_file   = "./provisioners/postinstall.yml"
  extra_arguments = [ "--diff", "--tags", "azure" ]
}
```

### Hyper-V provisioning 

* Install `hyper-v` daemons.

```hcl
provisioner "ansible" {
  only            = [ "qemu.hyper-v" ]
  playbook_file   = "./provisioners/postinstall.yml"
  extra_arguments = [ "--diff", "--tags", "hyper-v" ]
}
```

