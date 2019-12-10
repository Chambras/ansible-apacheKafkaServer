# KafkaServer

This ansible Playbook provides resources for installing, configuring and managing Apache Kafka. Installs Apache Kafka from a `.tgz` source and installs the appropriate configuration for your platform's init system.

It also installs `OpenJDK1.8`.

## Project Structure

```ssh
.
├── LICENSE
├── README.md
├── ansible.cfg
├── apache_kafka.yml
├── hosts
└── roles
    └── install
        ├── defaults
        │   └── main.yml
        ├── handlers
        │   └── main.yml
        ├── tasks
        │   └── main.yml
        └── templates
            ├── kafka.service.j2
            └── zookeeper.service.j2
```

## Requirements

### Platform Support

* RHEL 7.x
* CentOS 7.x

### Versions

* ansible 2.9.1

### Authentication

It uses key based authentication and it assumes you already have a key and you can configure the path using the _ansible_ssh_private_key_file_ variable in _`hosts`_ file.
You can create one using this command:

```ssh
ssh-keygen -t rsa -b 4096 -m PEM -C vm@mydomain.com -f ~/.ssh/vm_ssh
```

## Role Variables

This variables and their default values are located in `roles/install/defaults/main.yml`

```ssh
kafka_version: 2.3.0
kafka_scala_version: 2.12
kafka_user: kafkaAdmin
kafka_group: kafkaAdmin
kafka_root_dir: /opt
kafka_dir: '{{ kafka_root_dir }}/kafka'
```

## Usage

```ssh
ansible-playbook --syntax-check apache_kafka.yml
ansible-playbook apache_kafka.yml
```

## HOSTS file

The `hosts` file is the inventory file where you need to provide the IPs of the servers that need to be configured. You can also configure the SSH Key to use, username and SSH port.

You can create test servers using [this terraform script](https://github.com/Chambras/azure-terraform-vms)

## Authors

Marcelo Zambrana
