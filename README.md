# ansible-streaming-stack

This repo installs several streaming packages on an Amazon Web Services instance using an ansible playbook. Although the instructions here are for AWS, they should work equally well on other kinds of remote computers, provided they have the yum package manager installed.

This [companion article](http://datasciex.com/?p=161) explains how we can use streaming technology to monitor and control access to a website.

The playbook in ansible-streaming-stack is organized into these roles:
* common    - housekeeping
* flume     - Flume log stream package
* spark     - Spark streaming processor
* redis     - redis database

Each role has its own subdirectory structure containing tasks and supporting files.

## Prerequisites
1. A control computer (local or dedicated server) with Ansible, Maven, Git, and Jenkins.  
2. (optional) A local computer to connect to your dedicated server.
3. A running AWS instance with Amazon linux, a public IP address,  and an SSH key pair.
3. A file copy of the private SSH key on your local computer.

## Installation

1. Clone this repo on your control computer:

        git clone http://github.com/tomlamphier/ansible-streaming-stack.git
2. Copy the SSH private key to the project directory. Use the scp command to copy the file if you are working with a dedicated server.
3. Edit the hosts file; replace the xxx's with the public IP for the target AWS instance; set ansible_ssh_private_key_file variable to point to your private key.
4. Update the connect script to point to the private SSH key and the target AWS instance. Run it as a quick test of your connectivity to the AWS instance:

        ./connect
You should get an auth message on the first pass--simply say 'yes'.  If you see the AWS Amazon Linux welcome message, you are OK. Use logout to exit.
5. Run the playbook:
        ansible-playbook -i hosts playbook.yml
   This will install everything on the target computer.


## Reference
A blog post to bring you up to speed on Ansible: [Ansible Quick Start](http://datasciex.com/?p=230)
