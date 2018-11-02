# 1. install ansible
sudo apt -y install ansible sshpass

# 2. disable key check
sudo sed -i 's/#host_key_checking/host_key_checking/' /etc/ansible/ansible.cfg

# 3. with ssh key
ansible-playbook -b -i localhost, itm/code/deploy_docker.yml

# or

# 3. with password
ansible-playbook -k -b -i localhost, itm/code/deploy_docker.yml
