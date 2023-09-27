# Magento 2 docker image

1. register an access key at ![Adobe Commerce Market Place](https://commercemarketplace.adobe.com/customer/accessKeys/)
2. save the access key information in auth.json
3. run `docker build -f Dockerfile-web -t ricky/magento-web .` to build the web module
4. run `docker build -f Dockerfile-db -t ricky/magento-db .` to build the db module
5. run `docker compose up` to start
6. run `docker exec -ti magento-web-1 bash` to access the web container and execute these commands to initialise the web container
```
bin/magento setup:install --base-url=$BASE_URL --db-host=$DB_HOST --db-name=$DB_NAME  --db-user=$DB_USER  --db-password=$DB_PWD --admin-firstname=admin --admin-lastname=admin --admin-email=admin@admin.com  --admin-user=admin --admin-password=admin123 --language=en_AU --currency=AUD --timezone=$TZ --use-rewrites=1 --search-engine=$SEARCH_ENGINE --elasticsearch-host=$ELASTICSEARCH_HOST --elasticsearch-port=$ELASTICSEARCH_PORT
bin/magento indexer:reindex
bin/magento setup:static-content:deploy -f
bin/magento cache:flush
bin/magento sampledata:deploy
bin/magento setup:upgrade

```