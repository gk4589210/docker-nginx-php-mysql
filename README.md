# Docker-NGINX-PHP-MySQL
While this Docker setup is primarily intended for local development, it can be optimized for a production environment with some minor adjustments. Please see [Getting production ready](Getting-production-ready) for more information.

**To be improved**
1. Move away from MySQL. The Docker container for PHP already comes bundled with PostgreSQL which suits most purposes just fine.
2. Test building for production environments making sure that composer runs prior to copying all back end code into the PHP container.

## Makefile command reference
I have included some useful make commands that should make your life a little easier. After all, a lazy programmer that does not have to type a lot of characters is a happy programmer.

| Command         | Description                                      |
| --              | --                                               |
| clean           | Remove installed dependencies and database files |
| composer-update | Update installed vendor packages                 |
| docker-start    | Start all containers in detached mode            |
| docker-stop     | Stop all containers and remove Docker networks   |
| test            | Run PHPUnit tests inside the PHP container       |

## Prerequisites
The Docker setup in this repository is highly opinionated and, as it is predominantly used for local development, bundled with some frequently used extensions such as `pdo`, `pgsql` and PHP's `gd` library. This is simply to reduce time spend on configuration so I can get up and running more quickly. Think about your own technology stack and modify the configuration/container files accordingly.

While I have included a multi stage build process for building and copying the minized production files for the front end facing code (`Dockerfile.nginx`), I make use of Docker volumes to share source code between the host machine and Docker container. See `docker-compose.yml` for more information.

All the front end facing code is intended to live under the `front/` directory. The back end code should be kept under `back/`. For security purposes, the back end code is added to a location (`/var/www/hmtl/app`) that can only be accessed through the exposed `index.php` file that lives in `/var/www/hmtl/public/api/`. NGINX is configured to look for the index.php file at that location in the container's filesystem.

## Getting production ready
1. Determine which tools and technologies you depend on and include only those so as to reduce the overall size of your containers and improve build time. You can probably install these using the helper scripts that come with the Docker image for PHP or by adding additional images to the Docker compose file.
2. Copy all the files necessary to serve your back end code from the source machine to the Docker container. This requires you to modify the `Dockerfile.php`.
3. Remove the shared volumes from the `docker-compose.yml` file.
4. Test your setup to verify that everything is still working as expected. This might require you to sign into a running Docker container and check whether all the necessary files are there.

## Contributing
Is there anything that you found to be unclear or would like to see added or rectified? I encourage you to contribute by creating an issue or submitting a pull request. In order to submit a PR, simply:

1. Fork the project
2. Create a new branch with the proposed changes (`git checkout -b <branch name>`)
3. Commit the changes
4. Push the code
5. Create PR for code review

## License
Docker-NGINX-PHP-MySQL is licensed under the [MIT license](https://opensource.org/licenses/MIT)
