<p>version: &#39;3&#39; services: fontend: build: context: . dockerfile: ./docker/Dockerfile container_name: fontend working_dir: /var/www/html ports: - &#39;8000:80&#39;</p>

<p>volumes: - .:/var/www/html - ./docker/nginx_log:/var/log/nginx - ./docker/php-fpm/php-fpm.log:/var/log/php-fpm.log - ./docker/config/app.conf:/etc/nginx/conf.d/app.conf</p>

<p>depends_on: - backend links: - backend backend: image: mysql:5.6 container_name: backend ports: - &#39;3001:3306&#39; volumes: - ./docker/mysql:/var/lib/mysql</p>

<p>environment: MYSQL_ROOT_PASSWORD: 123456 links: - redis redis: image: redis restart: always command: redis-server --save 20 1 --loglevel warning --requirepass eYVX7EwVmmxKPCDmwMtyKVge8oLd2t81</p>

<p>container_name: redis ports: - &#39;6379:6379&#39; volumes: - redis:/data volumes: redis: driver: local</p>

<p>pass-mysql:123456 pass-redis:eYVX7EwVmmxKPCDmwMtyKVge8oLd2t81</p>

<p>set up env</p>

<p>REDIS_CLIENT=predis</p>

<p>REDIS_HOST=redis</p>

<p>REDIS_PASSWORD=eYVX7EwVmmxKPCDmwMtyKVge8oLd2t81</p>

<p>REDIS_PORT=6379</p>

<p>QUEUE_CONNECTION=redis</p>

<p>DB_CONNECTION=mysql</p>

<p>DB_HOST=backend</p>

<p>DB_PORT=3306</p>

<p>DB_DATABASE=api_backend</p>

<p>DB_USERNAME=root</p>

<p>DB_PASSWORD=123456</p>
## run <br/>
- docker build ./docker <br/>
- docker-compose up -d
