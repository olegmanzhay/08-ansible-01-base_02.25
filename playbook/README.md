Задание 1
---------------------------------------------------------------------------------------------------------------------------------------------------
```
ansible-playbook -i ./inventory/test.yml site.yml

ok: [localhost]

TASK [Print OS] *****************************************************************************************************************************************************************
ok: [localhost] => {
    "msg": "Ubuntu"
}

TASK [Print fact] ***************************************************************************************************************************************************************
ok: [localhost] => {
    "msg": 12
}

PLAY RECAP **********************************************************************************************************************************************************************
localhost                  : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
```

Задание 4
---------------------------------------------------------------------------------------------------------------------------------------------------
Вместо Centos7 ичпользовал образ alphine и настройку через Dockerfile делал  
Ubuntu поставил чистым и руками сделал ssh соединение 

Dockerfile alphine  https://github.com/olegmanzhay/08-ansible-01-base_02.25/blob/main/playbook/Dockerfile

Скорректировал inventory и playbook
- https://github.com/olegmanzhay/08-ansible-01-base_02.25/blob/main/playbook/inventory/prod.yml
- https://github.com/olegmanzhay/08-ansible-01-base_02.25/blob/main/playbook/site.yml

Запустил
```
ansible-playbook -i ./inventory/prod.yml site.yml

```
Задание 7-8
---------------------------------------------------------------------------------------------------------------------------------------------------
```
ansible-vault encrypt ./group_vars/deb/examp.yml 
ansible-vault encrypt ./group_vars/el/examp.yml 

ansible-playbook -i ./inventory/prod.yml site.yml --ask-vault-pass

```

Задание 10
---------------------------------------------------------------------------------------------------------------------------------------------------
Добавил в inventory
```
    local:
        hosts:
          localhost:
            ansible_connection: local
```
Задание 4*
---------------------------------------------------------------------------------------------------------------------------------------------------

docker pull pycontribs/fedora
docker build -t  ubuntu-ssh -f Dockerfile_ubuntu .
docker build -t  fedora-ssh -f Dockerfile_fedora .
docker build -t  alpine-ssh -f Dockerfile_alpine .

docker run -d -it -p 2223:22 --name ubuntu ubuntu-ssh:latest 
docker run -d -it -p 2224:22 --name fedora fedora-ssh:latest 
docker run -d -it -p 2222:22 --name alpine alpine-ssh:latest 

ansible-playbook -i ./inventory/prod.yml site.yml 


