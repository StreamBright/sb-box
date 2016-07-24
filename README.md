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

CentOS 7 base box is used for creating the local developer environment.

```bash
vagrant init centos/7 && vagrant box update
```

After downloading the latest CentOS 7 image (currently [1606.01](https://atlas.hashicorp.com/centos/boxes/7/versions/1606.01) ) the box can be created and started executing the following:

```bash
vagrant up
```

## Creating the cloud env

