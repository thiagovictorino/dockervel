
# Dockervel  
A docker-compose.yml file ready to be used in production or locally by Laravel apps. It helps you to create a production ready environment with SSL with [Let's Encrypt](https://letsencrypt.org) and [Traefik](https://github.com/containous/traefik/) as a reserve proxy.

With this repository, You will be able to set an environment with two containers running internally and exposing Traefik on por 80/443 that will forwards connection to each container depending of which url was reached.

For example:

	                                                      | → app-prouction
	http(s)://app.{staging}.domain.com:80/443 → traefik → |
	                                                      | → app-staging

## How to use

First of all you will need a server with Docker and docker-compose installed. There you will clone this repository.

Then, you will need to create a local network

    docker network create web

Now you need to create a .env file based on .env.example

    cp .env.example .env

Change the content of .env as you needed

Edit the file `traefik.toml` with your data. In this file is not possible to use .env. There are some comments that helps you what you need to change.

With everything is configured, now you are able to run

    docker-compose up -d

If everything was set rightly, You can access http(s)://app.your-domain.com.  

## Important

 - To makes it works locally with ssl you will need more configurations
   that is not in the scope of this package. You will need to do it by
   yourself.
 - You need to have a DNS configuration ready with domains/sub-domiains pointing to the host that you are try to config
 - Traefik will creates the SSL keys automatically. But maybe you will need to restart the container to renew those keys.
 - This package doesn't include a database container, You are free to add it on `docker-compose.yml`
 - How you are using a reverse proxy, You will probably will need to set [trusted proxies](https://laravel.com/docs/master/requests#configuring-trusted-proxies)  

## Credits

 - By default, this package uses [Ambiemtum](https://github.com/ambientum/ambientum) image for the Laravel containers.
