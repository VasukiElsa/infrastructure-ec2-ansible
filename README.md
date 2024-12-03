Creation of EC2-instance in AWS
=========

Template for creation of ec2-instance with public-ip address in aws.

Requirements
------------

 python >= 3.6
 boto3 >= 1.28.0
 botocore >= 1.31.0


Role Variables
--------------

Variables are referenced through Jinga Template in tasks/main.yaml file. You can give values for those variables in defaults/main.yml file. Then replace your aws access-key credentials in the group_vars/all/pass.yml file, which was encrypted with base64 format.


Example Playbook
----------------

Here we didn't use inventory file, because our control-node will act as a host and resources are created in aws through api using boto3 module. Our control-node(localhost).

    - hosts: localhost
      connection: local
      tasks:
        roles:
          - ec2-instance

Creating password authentication to the API,
   -> Creating a password for vault:

   $ openssl rand -base64 2048 > vault.pass

Add your aws credentials using the vault command,
 
    $ ansible-vault create group_vars/all/pass.yml --vault-password-file vault.pass
    (It will open the pass.yml file, then give your access key and secret-access-key.)

Run your playbook,

    $ ansible-playbook <playbook name> --vault-password-file vault.pass

         


