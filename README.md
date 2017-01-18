# Docker image for Magento 2

[![](https://images.microbadger.com/badges/image/netzkollektivgmbh/docker-magento2.svg)](https://microbadger.com/images/netzkollektivgmbh/docker-magento2)

[![Docker build](http://dockeri.co/image/netzkollektivgmbh/docker-magento2)](https://hub.docker.com/r/netzkollektivgmbh/docker-magento2/)

This image is a development environment for Magento 2 projects. You may either set up a **new Magento 2** installation with the provided install script or use the image with your **existing Magento project**.
Apart from the software neccessary to run Magento 2 it includes some useful tools we use a lot in our daily development. These are:

* vim *most important* 
* git 
* wget 
* curl 
* rsync 
* ssh 
* mysql-client 
* zip 
* ssmtp *needed by mailhog for local mail delivery*
* colordiff 
* cron *used to run Magento cron*

## Requirements

This image is meant to be used with docker-compose. The following files are needed to start the image:

* [docker-compose.yml](docker-compose.yml)
* [env](env)

You may adjust the docker-compose file to your needs.

## Usage

### Install Magento 2

If you want to install a fresh Magento installation, execute the `install` binary
```
docker-compose up -d
docker exec -ti {webContainerId} install
```

### Sample Data

To install Sample Data you need to set the env var `MAGENTO_INSTALL_SAMPLE_DATA`.
If unset, sample data will not be installed with the install script.

## Use with existing Magento 2 project

First you have to adjust the directory mapping in your docker-compose-yml by adding your Magento project. Assuming your project is available in `./web` add volumes as follows:
```
  web:
    volumes:
      - ./web:/var/www/html
```
After the change start your containers:
```
docker-compose up -d
docker exec -ti {webContainerId} init-project
```

## Settings

All settings are commented in the example [env](env) file.

## Utilities

The following utilities are intended to make your life easier:

* `install` is the install script to install Magento, either with sample data, or without, see above
* `enable-redis` changes the config of Magento so that it uses Redis for cache storage (much better performance, even for developing!)
* `set-permissions` sets permissions for Magento to work properly, according to your user settings
