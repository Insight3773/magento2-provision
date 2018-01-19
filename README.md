# Vagrant-заготовка для локальной разработки magento 2

## Окружение:
1. Virtualbox
2. Vagrant
3. Ansible
4. Unison
5. Composer

## Провижинг
1. В директории **provision** выполнить **cp Vagrant.yml.example Vagrant.yml**
2. Изменить настройки в файле **Vagrant.yml**. Параметры:

    `host` - локальное доменное имя (то, что нужно открывать в браузере)
    
    `ip` - ip-адрес в виртуальной сети, по которому будет доступна виртуальная машина.
    Нужно прописать сопоставление `host` и `ip` либо в hosts основной системы, либо использовать что-нибудь вроде dnsmasq
    
    `memory` - количество выделяемой виртуальной машине памяти (Мб)
    
    `synced_type` - тип синхронизации файлов. Этот параметр используется, если не использовать unison, но тогда нужно будет раскомментировать в Vagrantfile
    
3. Запустить виртуальную машину **vagrant up**. При первом запуске будет выполнен провижинг

# Разработка

## Установка платформы
Установка magento 2 достаточно хорошо описана в документации. 
Устанавливать в директорию `code`, т.к. именно эта директория синхронизируется в виртуальную машину и будет базовой директорией проекта

## Запуск unison-синхронизации

1. Для синхронизации необходимо установить unison
2. Синхронизация возможна только при работающей виртуальной машине
3. В отдельном окне терминала из директории проекта запустить `unison.sh`
4. Это окно терминала должно так и висеть на протяжении всего процесса разработки
5. В `unison.sh` жестко прописан `magento.test`, если нужен другой хост - меняйте 

## Создание нового приложения и быстрая переустановка существующего приложения
1. Войти в консоль виртуальной машины (**vagrant ssh**)
2. Изменить рабочую директорию **cd /var/www/vagrant/data**
3. Запустить `setup.sh`
4. В `setup.sh` жестко прописан `magento.test`, если нужен другой - меняйте
5. Настоятельно рекомендуется при developer-режиме отключить следующие типы кеша: layout, block_html, collections, full_page:
```
php bin/magento cache:disable layout block_html collections full_page
```
