# Magento 2 docker image

1. register an access key at ![Adobe Commerce Market Place](https://commercemarketplace.adobe.com/customer/accessKeys/)
2. save the access key information in auth.json
3. run `docker build -f Dockerfile-web -t ricky/magento-web .` to build the web module
4. run `docker build -f Dockerfile-db -t ricky/magento-db .` to build the db module
5. run `docker compose up` to start
6. run `docker exec -ti magento-web-1 bash` to access the web container and execute these commands to initialise the web container
```
bin/magento module:disable Magento_AdminAdobeImsTwoFactorAuth 
bin/magento module:disable Magento_TwoFactorAuth
bin/magento setup:install --base-url=http://localhost/ --db-host=db --db-name=magento2  --db-user=magento2  --db-password=magento2 --admin-firstname=admin --admin-lastname=admin --admin-email=admin@admin.com  --admin-user=admin --admin-password=admin123 --language=en_AU --currency=AUD --timezone=Australia/Melbourne --use-rewrites=1 --search-engine=elasticsearch7 --elasticsearch-host='elasticsearch' --elasticsearch-port='9200'
# bin/magento indexer:reindex
# bin/magento setup:static-content:deploy -f
# bin/magento cache:flush
bin/magento sampledata:deploy
bin/magento setup:upgrade

```