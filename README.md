# 1. install ansible/git
sudo apt -y install ansible sshpass git

# 2. disable key check
sudo sed -i 's/#host_key_checking/host_key_checking/' /etc/ansible/ansible.cfg

# 3. clone git
sudo mkdir -m 0777 /app && cd /app && git clone https://github.com/Kabanus/itm.git

# 3.1. deploy app with key
ansible-playbook -b -i localhost, /app/itm/content/ansible/deploy.yml

# or

# 3.2. deploy app with password
ansible-playbook -k -b -i localhost, /app/itm/content/ansible/deploy.yml

# 4. stop app
docker-compose -f /app/itm/content/docker/docker-compose.yml stop
