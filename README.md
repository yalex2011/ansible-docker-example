> Запуск роли возможен только после исправления криворукой разбивки диска образа VM!

Выполняем в консоли VM:

Правим GPT
`echo "Fix" > parted  /dev/sda`

Ресайзим lvm раздел
`parted /dev/sda resizepart 3 16,1GB`

Ресайз LVM
```
pvresize /dev/sda3
lvresize -l 100%FREE /dev/rhel/var
```
Ресайз xfs
`xfs_growfs -d /dev/rhel/var`

> Диск должен быть добавлен в VM
> /dev/sdb - 20GB !

Добовляем диск для teen pool'а
20GB

> При использовании нормальной виртуализации - это можно было сделать не руками...

#### Запускаем роль.

Фунцианал:
- after_create_vm
_Прописывает локальные репозитарии и отключает базовые. Отключает selinux_

- install_docker
_Установка Docker и копонентов (в том чичле и python модули)_

- thin_pool_create
_Создает teen pool и настраивает Docker для работы с ним_

- get_docker_image
_Устанавливает image из локального зеркала_
- build_docker_container
_Собирает image контейнера Flask App_
- docker_swarm
_Запускает Swarm_
- docker_stack_deploy
_Разворачивет проект Flask App в Swarm_
- docker_stack_check
_Проверка роботоспособности_

#### Смотрим на экран и ждем результата.

Примечание:

Тонкий пул & Докер, при тестировании показал не надежность. Использовать его я бы не стал.