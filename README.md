## Docker-сборка ###

### содержит: ###
- nginx:latest
- php:7.4
- mysql:8.0
- mariadb:10.4
- redis
- phpmyadmin
- adminer
- mailhog
- npm: node:13.7
- composer
- artisan




### Источник ###
https://tech.osteel.me/posts/docker-for-local-web-development-part-1-a-basic-lemp-stack


### Прописать по необходимости: ###
- в файле hosts 
    - windows - c:/Windows/System32/drivers/etc/hosts
    - MacOs, Linux - /etc/hosts
```
127.0.0.1 имя_сайта
```    


## Скрипт для запуска - ``` demo ```

Теперь нам нужно сделать этот скрипт доступным из любой точки терминала. Для этого добавьте следующую функцию в свой локальный файл .bashrc (или .zshrc, или что-нибудь еще в соответствии с вашей конфигурацией):
```
function demo {
    cd /PATH/TO/YOUR/PROJECT && bash demo $*
        cd -
}
```

Сохраните изменения и откройте новое окно консоли или sourceфайл, чтобы они вступили в силу:
```
source ~ / .bashrc
```
#### ``` можно просто вызывать скрипт в корне директории ```
```
bash demo
```
 Выдаст весь список доступных комманд.

## Github
После клонирования - удалить ``` .git ``` в корне 
```
rm -rf .git
```


