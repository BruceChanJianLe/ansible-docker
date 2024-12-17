# Ansible Docker

This is an Ansible playbook that assist the installation of docker and NVIDIA docker.


## Install Dependencies
```bash
sudo apt install ansible git -y
```

## Installation

```bash
ansible-pull -U https://github.com/brucechanjianle/ansible-docker -K
```

## Verification

```bash
docker run hello-world
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
