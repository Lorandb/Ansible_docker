# Ansible_docker

## Application descirption
A basic note taking app from the [Docker Getting Started Guide](https://docs.docker.com/get-started/02_our_app/)

## How it set it up?
1. Need to have an server with ansible installed and configured.
<code> ansible --version </code> will show the config file location.

Output:

`config file = /etc/ansible/ansible.cfg`

The config file will have an invetory file, in our case is:
`inventory = /etc/ansible/hosts`

Invetory file should contain the target server ip, the port variable parameter and the python version used:

`[servers]`

`server1 ansible_host=134.209.247.186`

`[all:vars]`

`ansible_python_interpreter=/usr/bin/python3`

`port_number=2800`

3. Configure ssh connection on the target server; so that no password is required.
4. Configure the ansible invenotry to have the correct ip adress of the target server. Modify the file /etc/ansible/hosts
5. Modify the port_number variable to the port on which the app shoud listen. Modify the file /etc/ansible/hosts
6. Run the ansible playbook with the command below

<code> ansbile-playbook docker_playbook.yml</code> -u root

5. Check if 2 docker containers are running on the target host:

`docker ps -a`

Output:


`root@ubuntuansibleslave:~# docker ps -a`

`CONTAINER ID   IMAGE            COMMAND                  CREATED        STATUS        PORTS                                                  NAMES`

`d07fb03d165f   node:12-alpine   "docker-entrypoint.s…"   36 hours ago   Up 36 hours   0.0.0.0:2800->3000/tcp, :::2800->3000/tcp              to-do-app_web_1`

`b05c4bac5dbb   mysql:5.7        "docker-entrypoint.s…"   36 hours ago   Up 36 hours   0.0.0.0:3306->3306/tcp, :::3306->3306/tcp, 33060/tcp   to-do-app_mysql_1`


6. Make sure no firwall is blocking the port from external connections.
7. Check the web app with the browser using the link `host:portnumber` configured in the `/etc/ansible/hosts` file
8. The application can be accees from the internet using this link:

`http://134.209.247.186:2800/`
