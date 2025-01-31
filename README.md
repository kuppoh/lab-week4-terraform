# lab-week4-terraform
---
Austin Park | Keziah Wacnang

### Task 1
---
Create new SSH keypair using the following command:
`ssh-keygen -t ed25519 -f acit4640_terraform -C "acit4640_terraform key"`

Adding the public key to the included cloud-init config file:
* edit the `cloud-config.yaml` file to add our public key

```yaml

#cloud-config
users:
  - name: web
    primary_group: web
    groups: wheel
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - <public-key>

```

To get the ssh public key content:
* `cat ~/.ssh/acit4640_terraform.pub`
* we then copied it over to the `<public-key>` field in the `cloud-config.yaml` file

Then we added the packages we needed to install: `nginx` and `nmap`:
```yaml

users:
  - name: web
    primary_group: web
    groups: wheel
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh_authorized_keys:
      - <ssh-key-here>

package_update: true
package_upgrade: true
packages:
  - nginx
  - nmap
```
* this will update and upgrade the packages first before installing the following packages.

To check if the config file is validated:
* `cloud-init schema -c cloud-config.yaml --annotate`

Sources:
* https://cloudinit.readthedocs.io/en/latest/explanation/about-cloud-config.html
* https://cloudinit.readthedocs.io/en/latest/howto/debug_user_data.html#check-user-data-cloud-config

### Task 2
---


