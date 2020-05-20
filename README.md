# Ansible Playbook Template
Server Provisioning with Ansible, Vagrant and Packer.

## Feature
- Local environment is Vagrant.
- Execute Ansible and Packer with docker-compose.
- Test with Testinfra.
- Create AMI on AWS with Packer.
- Execute server provisioning with Ansible.

## Requirements
- docker
- docker-compose
- vagrant
- virtualbox

## Advance preparation
### [Vagrant Integration](https://testinfra.readthedocs.io/en/latest/examples.html?highlight=vagrant#integration-with-vagrant)
If you want to test Vagrant machine from your own terminal, execute the following command.

```
$ pip install testinfra paramiko
$ vagrant ssh-config > .vagrant/ssh-config
$ py.test -v --hosts=web --ssh-config=.vagrant/ssh-config tests
```

## Usage
### Local execute with Vagrant
#### up
```
$ vagrant up web
```

#### provision
```
$ vagrant provision web
```

#### ssh
```
$ vagrant ssh web
```

### Create AMI on AWS with Packer
#### lint
```
$ docker-compose run --rm packer validate packer/web.json
```

#### inspect
```
$ docker-compose run --rm packer inspect packer/web.json
```

#### build
```
$ docker-compose run --rm packer build packer/web.json
```

### Run Ansible Playbook
#### lint
```
$ docker-compose run --rm ansible-playbook -i inventory web.yml --syntax-check
```

#### run
```
$ docker-compose run --rm ansible-playbook -i inventory web.yml
```
