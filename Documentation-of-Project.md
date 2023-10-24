Project Documentation: Automated Provisioning of Ubuntu Servers with LAMP Stack

Objective

The objective of this project is to automate the provisioning of two Ubuntu-based servers, named "Master" and "Slave," using Vagrant. On the Master node, a bash script is created to automate the deployment of a LAMP (Linux, Apache, MySQL, PHP) stack. Laravel is used as the PHP framework used in the PHP application that's cloned and deployed. Laravel simplifies building web applications, facilitating web development and interaction with the LAMP stack, enhancing code readability and reusability while ensuring a web application accessible via the VM's IP address.This script should clone a PHP application from GitHub, install all necessary packages, and configure the Apache web server and MySQL. The goal is to ensure the bash script is reusable and readable.

Using an Ansible playbook, the project involves executing the bash script on the Slave node and verifying that the PHP application is accessible through the VM's IP address. Additionally, a cron job is created to check the server's uptime every day at 12 am.


A bash script to automate both the master and slave1 machine was created. This script automates the installation process for a master and slave Ubuntu vagrant machine, allowing for a seamless setup of a LAMP stack. The following components are required for successful execution:

Vagrant
Virtual Box
Slave & Master Machine Specifications:

Memory: 1024 MB
CPUs: 2
Slave Machine Configuration: The slave1 machine will contain the following specifications:

Name: slave1
Image: ubuntu/focal64
Network Settings:
Private Network
IP Address: "192.168.20.11"

Master Machine Configuration: The master machine will have the following specifications:

Host Name: master
Image: ubuntu/focal64
Network Settings:
Private Network
IP Address: "192.168.20.10"



                                    bash-script.sh file
This script facilitates the automated deployment of a Laravel application on the master node. It carries out the following tasks:

- Updates and upgrades the server.
- Installs the LAMP stack (Linux, Apache, MySQL, PHP).
- Configures Apache and creates a virtual host for the Laravel application.
- Installs Composer, a PHP package manager. 
- Clones the Laravel application from GitHub and installs its dependencies.
- Sets appropriate file permissions for the application.
- Configures the MySQL database by creating a user and granting privileges.
- Sets up environment variables for optimal functioning of the Laravel application.
- Executes specific commands to optimize the application's configuration and perform database migrations.

This script simplifies and speeds up the deployment of a Laravel application's configuration while also making it reuseable for efficient depolyment and database migrations.

                                    Ansible-Playbook
The Ansible playbook automates the execution of a bash script on the "Slave1" node, deploying a PHP application cloned from GitHub and ensuring its accessibility through the VM's IP address. It also creates a cron job to check server uptime at 12 am. The playbook simplifies server management, enhances the reliability of the deployment process, and provides a consistent environment.

Ansible.cfg file - contains essential settings. 

    Inventory file - This line specifies the path to the Ansible inventory file, where target hosts are listed. The inventory file helps Ansible identify which hosts the target machine "Slave1" vm ip addres to manage.
 
    private_key_file ~/.ssh/id_rs :specifies the SSH private key for authentication,when connecting to remote hosts. It points to the default SSH key file in the master to the slave machine in other to simplify access.

Site.yaml - automates tasks on remote hosts. It performs the following actions:

Updates and upgrades the server by running apt update and apt upgrade.
Sets a daily cron job to check server uptime at 12 am, storing the result in /var/log/uptime_check.log.
Copies a bash script named "laravel-slave.sh" to the home directory into the master machine.
Configures execute permissions for the script.
Runs the "laravel-slave.sh" script with specific parameters.

files - 
    "Laravel-Slave.sh automates the setup process for a LAMP (Linux, Apache, MySQL, PHP) stack, Composer, and Laravel application on a server. It first updates and upgrades the server before installing all necessary software components. Then, it handles the configuration of Apache, creates a virtual host specifically for Laravel applications, and clones a designated repository from GitHub. The script also takes care of managing dependencies for the application and setting up database configuration. Additionally, it generates environment variables to ensure smooth functionality. Finally, it configures and executes Laravel commands tailored to optimize the performance of the application. With its efficient deployment process, this script can be reused for streamlined development environment setups."


To ensure the successful execution of the script, the following three conditions must be met:

1. **.env File Configuration**: Make sure to configure the `.env` file with the correct username and password. Both the username and the database name should have the same credentials.

2. **MySQL Execution**: When running the script, use the following command: `./laravel.sh dimeji awoyemi12` where `dimeji` is the username and `awoyemi12` is the password. Ensure that these credentials match the ones set in the MySQL configuration.

3. **IP Address Configuration**: Modify the IP address in the Apache configuration to match the server's IP address. This ensures that you can access the Laravel application via the server's IP address.

By adhering to these conditions, you can run the script smoothly and set up the Laravel server as intended.