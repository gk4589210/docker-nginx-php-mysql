# Docker-NGINX-PHP-MySQL
This Docker setup is optimized for local development and is still a work in progress.

### Makefile commands
| command         | description                                      |
| --              | --                                               |
| clean           | Remove installed dependencies and database files |
| composer-update | Update installed vendor packages                 |
| docker-start    | Start all containers in detached mode            |
| docker-stop     | Stop all containers and remove Docker networks   |
| test            | Run PHPUnit tests inside the PHP container       |

### Prerequisites
This repository contains the necessary Docker configuration that allows you to host your front- and back end code. By default, NGINX serves the front end code from the `/front` directory. The PHP code lives inside the `/back` directory. Take a look at the `docker-compose.yml` file or the playground-laravel repository at the URL below:

https://github.com/99linesofcode/playground-laravel

### Production
The NGINX container is configured to build and deploy your front end code automatically. You can safely remove the shared volume on ` line 11` of the `docker-compose.yml` file in production environments. None of the source files for your React.Js application are copied to the Docker container.

For security purposes, the back-end code lives in an inaccessible location on the server, outside the public directory (`/var/www/hmtl/app`). It can only be accessed through the exposed `index.php` file that lives in `/var/www/hmtl/public/api/`.

### Contributing
We encourage you to contribute to this repository by opening issues and submitting pull requests. In order to submit a PR, simply:

1. Fork 
1. Branch
1. Commit
1. Push
1. PR

### License

Docker-NGINX-PHP-MySQL is licensed under the [MIT license](https://opensource.org/licenses/MIT)
