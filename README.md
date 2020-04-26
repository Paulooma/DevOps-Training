# DevOps Training

## Git

How to use git :

``` shell
# to add a file in the index I can use the command :
git add README.md
# to commit a file into the repo I can use the command :
git commit -m "my commit message"
# to push your commits to 'origin' you need to :
git push
```

Useful links :

- [Git Flow](http://danielkummer.github.io/git-flow-cheatsheet/index.fr_FR.html)
- [GitHub Flow](https://guides.github.com/introduction/flow/)
- [Training Kit](https://github.github.com/training-kit/)
- [Etienne Deneuve Blog](https://etienne.deneuve.xyz/2018/06/23/git-pour-ops-par-un-ops/)

## Packer

To use Packer we need to have a json file like this one :

``` json
{
  "variables": {
    "client_id": "{{env `ARM_CLIENT_ID`}}",
    "client_secret": "{{env `ARM_CLIENT_SECRET`}}",
    "subscription_id": "{{env `ARM_SUBSCRIPTION_ID`}}"
  },
  "builders": [
    {
      "type": "azure-arm",
      "client_id": "{{user `client_id`}}",
      "client_secret": "{{user `client_secret`}}",
      "subscription_id": "{{user `subscription_id`}}",
      "os_type": "Linux",
      "image_publisher": "Canonical",
      "image_offer": "UbuntuServer",
      "image_sku": "16.04-LTS",
      "managed_image_resource_group_name": "packertest",
      "managed_image_name": "MyUbuntuImage",
      "azure_tags": {
        "dept": "engineering",
        "task": "image deployment"
      },
      "location": "West Europe",
      "vm_size": "Standard_DS2_v2"
    }
  ],
  "provisioners": [
    {
      "execute_command": "chmod +x {{ .Path }}; {{ .Vars }} sudo -E sh '{{ .Path }}'",
      "inline": [
        "apt-get update",
        "apt-get upgrade -y",
        "/usr/sbin/waagent -force -deprovision+user && export HISTSIZE=0 && sync"
      ],
      "inline_shebang": "/bin/sh -x",
      "type": "shell"
    }
  ]
}
```


## Terraform
