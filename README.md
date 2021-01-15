# Packstack ( devstack ) installation using ansible
## Additional information
### OS_Family: RedHat
1.1 Hardware requirements :

	▪	RAM 16GB
	▪	CPU 4
	▪	Disk: 100 GB

1.2 Software requirements 

	▪	Redhat system should be registered with your satellite sever to subscribe and enable the required repositories.
	▪	enable the base repos 
	▪	e.g: For RHEL 8
	▪	rhel-8-for-x86_64-appstream-rpms
	▪	rhel-8-for-x86_64-baseos-rpms
	▪	rhel-8-for-x86_64-supplementary-rpms        

## Installation steps :

1. Clone repository with below command on your ansible server.

   git clone < repository_name > 
   
2. create vm as per your usecase like os flavour can  be RHEL or CentOS .
3. Change the "ad_addr" in the env_variables file with the IP address of your created vm.
4. provide your vm ip in inventory file along with your user and password in below format. Note: Below is just a sample IP, may be vary. 

   10.20.30.40 ansible_ssh_user=root ansible_ssh_pass=Passw0rd@1234
   
5. check once whether your vm is accessible from ansible server with below command , if you get pong response like "pong" this mean your vm is accessible.
   
   ansible all -m ping
   
   10.20.30.40 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/libexec/platform-python"
    },
    "changed": false,
    "ping": "pong"
    }
   
6. Run the following command to start the installation.

   ansible-playbook setup_packstack.yml

7. once the installation is completed successfully, it will create keystonerc_admin file on packsack server in /root directory where you can find the username and      password details to login to packstack/openstack dashboard

   http://<vm_ip>/dashboard
   
8. at the end of execution of above ansible playbook , you will get the username and password as well.
9. After completion of installation you can login to packsack instance and access the rc file with below commands and validate your installation.
     
   source /root/keystonerc_admin

10. Below are the few openstack commands to validate setup

   openstack image list
   openstack server list
   openstack flavor list
   openstack user list

11. For more hands-on to packsack, you can access below link and start working on networking stuffs.

    https://www.rdoproject.org/networking/floating-ip-range/


# Reference:

https://docs.openstack.org/install-guide/environment-packages-rdo.html
https://www.rdoproject.org/install/packstack/
