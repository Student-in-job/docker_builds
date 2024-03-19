## Alpine Apache + PHP 8.2 + Mysql (MariaDB)

This is configuration for running PHP 8.2 configured for Laravel 10 usage with Redis


## Files
- docker/apache2/httpd.conf

```
Required for different configuration in apache2 service and enabling or disabling Apache modules 
```

## Installation
Copy all contents of folder to the root of your PHP project.
Open docker-compose.yml and change mounting of requred storage folders name of project and path to the .ENV file.
Use command to run container:
```
docker-compose up -d
```
or (if you want to rebuild container image each time):
```
docker-compose up --build --force-recreate -d
```
