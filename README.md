### Dev env for planner application:
It's client-server application contains from two independent parts.

#### Setup:
Add hosts:  
`127.0.0.1 api.planner.local app.planner.local`  

Start docker containers:
```bash
cd ..
git clone git@github.com:andreyserdjuk/planner-gql-api.git planner
git clone git@github.com:andreyserdjuk/simple-planner-client.git planner-client

cd -
docker-compose up -d
docker-compose exec -u docker fpm bin/console do:da:cre
docker-compose exec -u docker fpm bin/console do:mi:mi
docker-compose exec -u docker fpm bin/console do:fi:lo
```

#### Disable xdebug in container
```bash
docker-compose exec fpm bash -c 'sed -i -e "s/^zend_e/;zend_e/g" /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini'
docker-compose restart fpm
```

#### Enable xdebug in container
```bash
docker-compose exec fpm bash -c 'sed -i -e "s/^;zend_e/zend_e/g" /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini'
docker-compose restart fpm
```
