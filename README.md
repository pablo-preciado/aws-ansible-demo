# Creating VM's in AWS with Ansible

## Introduction

In this repo we will have the playbooks for creating Virtual Machines and the basic infrastructure needed for creating them in AWS.

This is mean to be used by Redhatters or Red Hat partners having access to RHPD as we will deploy an AWS blank environment and then use the resource group that Red Hat provides to create all the other resources.

## Preparing the environment

You need to export the values for environment variables with the values related to your Azure environment:

```
export AWS_ACCESS_KEY_ID='AK123'
export AWS_SECRET_ACCESS_KEY='abc123'
```

The ansible-navigator.yml is already configured so it passes the values of those ENV variables to the execution environment.

Then clone this repo and change to the directory of this repo. This is very important as you need to be in this directory so ansible-navigator catches the config from the files here. These files configure ansible-navigator so it can pass the ENV variables to the execution environment among other things.

Log into quay.io with your Red Hat employee account (you need to have the employee account to use the Execution Environment):

```
podman login quay.io
```

Once there you can just modify the values of vars.yml and then run ansible-navigator:
```
ansible-navigator run aws-infra-create.yml -e @vars.yml
```
Then deploy your virtual machines:
```
ansible-navigator run aws-vm-create.yml -e @vars.yml
```

Use the same command but changing the playbook for differen operations such as stopping, starting or deleting your virtual machines. This repo also provides the playbook for deleting all your infra.