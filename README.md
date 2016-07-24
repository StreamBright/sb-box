# StreamBright - Box

This is a repository to easily create and manage local or remote development environments for machine learning and data science using opensource tools.

## Basics

### Local env

For the local environment there are two tools to install on the host operating system:

- [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
- [Vagrant](https://www.vagrantup.com/)

After installing the requirements there is a Vagrant file to run that creates the initial guest system using CentOS. When the operating system is up the required libraries (Pandas, NumPy, etc.) are installed and configured by Ansible. At the end Jupyter is installed and started.

### Cloud Env

For the cloud environment only the Ansible part applies, the machine learning libraries are installed and configured by the sb-box playbook. Please be advised that even though Amazon offers free tier usage there are usually cost implications of using cloud services.

## Creating the local env

### Provisioning Operating System

CentOS 7 base box is used for creating the local developer environment.

```bash
vagrant init centos/7 && vagrant box update
```

After downloading the latest CentOS 7 image (currently [1606.01](https://atlas.hashicorp.com/centos/boxes/7/versions/1606.01) ) the box can be created and started executing the following:

```bash
vagrant up
```

After successfully created the virtual instance we can log into it by:

```bash
ssh centos@10.20.30.40
```

### Installing Data Science & Machine Learning Stack

Installation is automated by Ansible, testing our setup can be done by pinging the box.

```bash
$ ansible local -m ping -i hosts.local
The authenticity of host '10.20.30.40 (10.20.30.40)' can't be established.
RSA key fingerprint is aa:bb:aa:bb:aa:bb:aa:aa:bb:aa:bb:aa:bb:aa:bb:aa.
Are you sure you want to continue connecting (yes/no)? yes
10.20.30.40 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
```
Running the following will configure everything that we need:

```bash
$ ansible-playbook sb-local-stack.yml -i hosts.local
```

After running Ansible Jupyter can be started by:

```bash
host$ ssh centos@10.20.30.40
guest$ source py2-env/bin/activate 
guest$ jupyter notebook
```

[Accessing Jupyter](http://10.20.30.40:8888/)

## Creating the cloud env

