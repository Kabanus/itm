# itm

# install ansible
sudo apt -y install ansible sshpass
sudo sed -i 's/#host_key_checking/host_key_checking/' /etc/ansible/ansible.cfg

# with ssh key
ansible-playbook -b -i localhost, itm/code/deploy_docker.yml

# with password
ansible-playbook -k -b -i localhost, itm/code/deploy_docker.yml
