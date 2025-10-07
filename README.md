# Ansible Docker

This is an Ansible playbook that assist the installation of docker and NVIDIA docker.


## Package Dependencies
```bash
sudo apt install ansible git -y
```

## Installation

```bash
ansible-pull -U https://github.com/brucechanjianle/ansible-docker -K
```

## Verification

```bash
docker run --rm hello-world
docker run --rm --gpus all nvidia/cuda:12.2.0-base-ubuntu20.04 nvidia-smi
```

## Post Installation

Note that after installing docker, you are required to reboot or re-login to
activate the re-evaluation of groups in order to run it without
root privilleges.

For the impatient, you may also activate the changes by running:
```bash
newgrp docker
```

## Deprecation Warning

Due to the fact that docker still stores its trusted key in the legacy trusted.gpg kering (/etc/apt/trusted.gpg).
Starting from ubuntu 22.04, this warning will appear everytime you do an `apt update`.
There's a proper way to remove the warning and a dirty way.
But of course, the best way, is to way for docker to store their key in the non legacy place (/usr/share/keyrings).


It's not really an issue, since it is only a warning.
But if you are inclinced to remove it, like me, there's a great article that talks about this.
https://itsfoss.com/key-is-stored-in-legacy-trusted-gpg/

For the impatient:

List and identify the deprecate key.
```bash
sudo apt-key list
# /etc/apt/trusted.gpg
# --------------------
# pub   rsa4096 2017-02-22 [SCEA]
#       9DC8 5822 9FC7 DD38 854A  E2D8 8D81 803C 0EBF CD88
# uid           [ unknown] Docker Release (CE deb) <docker@docker.com>
# sub   rsa4096 2017-02-22 [S]
# ...
```

Obtain the last 8 character, and export it!

```bash
sudo apt-key export 0EBFCD88 | sudo gpg --dearmour -o /etc/apt/trusted.gpg.d/docker.gpg
```
