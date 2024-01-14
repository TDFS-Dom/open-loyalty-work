UPGRADE FROM 3.0 to 3.1
=======================

Before you upgrade
------------------

Before you start upgrading, always backup your data in case something goes wrong.

1. Backup your data from PostgreSQL database

`docker exec -t open_loyalty_db pg_dumpall -U openloyalty > dump.sql`

2. If you have a lot of data in Elasticsearch, it's a good idea to create a snapshot to speed up process of recovering data.

https://www.elastic.co/guide/en/elasticsearch/reference/2.2/modules-snapshots.html

If somehow you can't do a snapshot, you can always rebuild data in Elasticsearch using commands

`docker exec -it open_loyalty_backend bash`

`su www-data`

`bin/console oloy:user:projections:purge`

`bin/console oloy:utility:read-models:recreate`

Note that recreating a lot of data may take a while and is not as fast as using snapshots.

Upgrading to 3.1.*
------------------

1. Upgrade Open Loyalty version

The first step depends on how you use Open Loyalty version.

2. Login to the PHP container

`docker exec -it open_loyalty_backend bash`

`su www-data`

3. Remove cache

`rm -rf var/cache/*`

4. Update parameters.yml file

4a. You can manually check new parameters by checking a file app/config/parameters.yml.dist and copy newly added values to the app/config/parameters.yml

4b. You can automatically generate a new app/config/parameters.yml file using composer

`composer install`

5. Create a new table for Snapshots feature

`bin/console broadway:snapshoting:schema:init -n`

6. Migrate data

`phing migrate`

7. Add newly added translations to the Settings -> Translations from https://github.com/DivanteLtd/open-loyalty-framework/blob/master/src/OpenLoyalty/Bundle/SettingsBundle/DataFixtures/ORM/translations/english.json 

I have an older version
-----------------------

If you have an older version than 3.0.* then you have to go through each version and upgrade according to UPGRADE-*.md file for each version.
