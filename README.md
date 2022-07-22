version: '3'
services:
    fontend:
        build:
            context: .
            dockerfile: ./docker/Dockerfile
        container_name: fontend
        working_dir: /var/www/html
        ports:
            - '8000:80'
        volumes:
            - .:/var/www/html
            - ./docker/nginx_log:/var/log/nginx
            - ./docker/php-fpm/php-fpm.log:/var/log/php-fpm.log
            - ./docker/config/app.conf:/etc/nginx/conf.d/app.conf
        depends_on:
            - backend
        links:
            - backend
    backend:
        image: mysql:5.6
        container_name: backend
        ports:
            - '3001:3306'
        volumes:
            - ./docker/mysql:/var/lib/mysql
        environment:
            MYSQL_ROOT_PASSWORD: 123456
        links:
            - redis
    redis:
        image: redis
        restart: always
        command: redis-server --save 20 1 --loglevel warning --requirepass eYVX7EwVmmxKPCDmwMtyKVge8oLd2t81
        container_name: redis
        ports: 
            - '6379:6379'
        volumes:
            - redis:/data
volumes:
    redis:
        driver: local
        
pass-mysql:123456
pass-redis:eYVX7EwVmmxKPCDmwMtyKVge8oLd2t81
set up env
REDIS_CLIENT=predis
REDIS_HOST=redis
REDIS_PASSWORD=eYVX7EwVmmxKPCDmwMtyKVge8oLd2t81
REDIS_PORT=6379
QUEUE_CONNECTION=redis
DB_CONNECTION=mysql
DB_HOST=backend
DB_PORT=3306
DB_DATABASE=api_backend
DB_USERNAME=root
DB_PASSWORD=123456
