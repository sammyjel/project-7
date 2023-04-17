# DEVOPS TOOLING WEBSITE SOLUTION
In this projject I implemented a web solution for a DevOps team using LAMP stack with remote Database and NFS servers

We will use the following components in this project:

-Infrastructure: Amazon Web Services -3 Linux webservers: Red Hat Enterprise Linux 8 -A database system, such as Ubuntu 20.04 and MySQL -Red Hat Enterprise Linux 8 as a storage system -PHP as a programming language -GitHub code source

Examine the architecture of the answer we want to build below:
![thestrucure](./images/project%20structure.png)

To start SET UP 

Start four EC2 instances using the RHEL 8 operating system.

Give them the following names: Web1, Web2, Web3, and NFS-svr.

Launch a second EC2 instance running Ubuntu 20.04 with the name DB.-svr

Attach three volumes, each 10 Gib, to the NFS-svr server.

Create volumes according to the directions in [project-6](https://github.com/sammyjel/project-6/blob/main/project-6.md) repository, then attach them to the appropriate instance.

Create the following logical volumes using this [guide](https://github.com/sammyjel/project-6/blob/main/project-6.md):

lv-apps
lv-logs
lv-opt

To act as mount points for the newly formed logical volumes, create the /mnt directory.

Install lv-apps in /mnt/apps. (this will be used by the webbservers)

Install lv-logs in /mnt/logs (this will be used by webserver logs)

Install lv-opt in /mnt/opt (this will be used by jenkins in the next project)

NOTE: If you carefully followed the instructions, running the command `sudo lsblk` should have produced the output shown below.

![mnt vol](./images/Screenshot%202023-04-17%20091715.png)

Using the xfs filesystem, format the logical volume.

`mkfs /dev/webdata-vg/lv-apps -t xfs`

`mkfs /dev/webdata-vg/lv-logs -t xfs`

`mkfs /dev/webdata-vg/lv-opt -t xfs`

Open your NFS-svr terminal and run the following instructions sequentially:

`sudo yum -y update`

`sudo yum install nfs-utils -y`

`sudo systemctl start nfs-server.service`

`sudo systemctl enable nfs-server.service`

`sudo systemctl status nfs-server.service`

