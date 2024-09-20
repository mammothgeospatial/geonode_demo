# Geonode_Demo

### Add .env file

1. Add provided .env file in root directory

### Start your server using Docker

You need Docker 1.12 or higher, get the latest stable official release for your platform.
Once you have the project configured run the following command from the root folder of the project.

1. Run `docker compose` to start

    ```bash
    docker compose build --no-cache
    docker compose up -d
    ```

    Note: if the ``` docker compose up ``` command returns an error after the first build, then run ``` docker compose stop ``` and ``` docker compose up ``` again.

2. Access the site on http://localhost/

### Credentials

Default credentials are:

1. Geonode (../account/login/)

```
username: admin
password: admin
```

2. Geoserver (.../geoserver/web)

```
username: admin
password: see GEOSERVER_ADMIN_PASSWORD value in .env
```

If the admin geoserver credentials are changed they need to be edited in the .env so that geonode can connect.


## Run the instance on a public site

### Preparation of the image (First time only)

**NOTE**: In this example we are going to publish to the public IP http://123.456.789.111

```bash
vim .env
  --> replace localhost with 123.456.789.111 everywhere
```

### Startup the image

```bash
docker compose up --build -d
```

### Stop the Docker Images

```bash
docker compose stop
```

## Backup and Restore from Docker Images

### Run a Backup

```bash
SOURCE_URL=$SOURCE_URL TARGET_URL=$TARGET_URL ./geonode_demo/br/backup.sh $BKP_FOLDER_NAME
```

- BKP_FOLDER_NAME:
  Default value = backup_restore
  Shared Backup Folder name.
  The scripts assume it is located on "root" e.g.: /$BKP_FOLDER_NAME/

- SOURCE_URL:
  Source Server URL, the one generating the "backup" file.

- TARGET_URL:
  Target Server URL, the one which must be synched.

e.g.:

```bash
docker exec -it django4geonode_demo sh -c 'SOURCE_URL=$SOURCE_URL TARGET_URL=$TARGET_URL ./geonode_demo/br/backup.sh $BKP_FOLDER_NAME'
```

### Run a Restore

```bash
SOURCE_URL=$SOURCE_URL TARGET_URL=$TARGET_URL ./geonode_demo/br/restore.sh $BKP_FOLDER_NAME
```

- BKP_FOLDER_NAME:
  Default value = backup_restore
  Shared Backup Folder name.
  The scripts assume it is located on "root" e.g.: /$BKP_FOLDER_NAME/

- SOURCE_URL:
  Source Server URL, the one generating the "backup" file.

- TARGET_URL:
  Target Server URL, the one which must be synched.

e.g.:

```bash
docker exec -it django4geonode_demo sh -c 'SOURCE_URL=$SOURCE_URL TARGET_URL=$TARGET_URL ./geonode_demo/br/restore.sh $BKP_FOLDER_NAME'
```

## Increasing PostgreSQL Max connections

In case you need to increase the PostgreSQL Max Connections , you can modify
the **POSTGRESQL_MAX_CONNECTIONS** variable in **.env** file as below:

```
POSTGRESQL_MAX_CONNECTIONS=200
```

In this case PostgreSQL will run accepting 200 maximum connections.
