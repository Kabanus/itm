После выполнения инструкций получаем:
1. Три работающих контейнера:
 - nginx
 - php-fpm
 - mysql
 2. Изменяемые файлы располагаются локально в директории /app
  - ansible: скрипт развертывания
  - docker: скрипт запуска контейнеров
  - mysql: база данных
  - nginx: конфигурация сайта
  - wordpress: движок сайта
3. Создается учетная запись developer с паролем password которая может выполнять команду docker без sudo и имеет право на запись в /app
4. Доступ к базе данных "mysql -u developer -h 127.0.0.1 --password=password --database=wordpress".
5. Доступ к сайту http://ip-address

Дополнения (ИМХО):
1. На мой взгляд более целесеобразно монтировать директорию /app по nfs с СХД(sAN), желательно SSD.
2. Касательно беспростойносй публикации - в данный момент я не вижу универсального способа (но не говорю что его нет).

# 1. Установка ansible и git
sudo apt -y install ansible sshpass git

# 2. Отключение проверки ключа хоста
sudo sed -i 's/#host_key_checking/host_key_checking/' /etc/ansible/ansible.cfg

# 3. Клонирование git
sudo mkdir -m 0777 /app && cd /app && git clone https://github.com/Kabanus/itm.git

# 3.1. Разворачивание с ключем
ansible-playbook -b -i localhost, /app/itm/content/ansible/deploy.yml

# или

# 3.2. Разворачивание с паролем
ansible-playbook -k -b -i localhost, /app/itm/content/ansible/deploy.yml

# 4. Остановка работы
sudo docker-compose -f /app/itm/content/docker/docker-compose.yml stop
