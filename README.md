# DEMP

My dev environment tailored to laravel and php web dev projects - Docker, Nginx, MySQL, PHP-FPM

## Getting Started

1. Clone the repository
2. Clone your project into or add a directory called 'web' at the root of the repository (already ignored in .gitignore)
3. Edit ./container/nginx/sites/site.conf or replace it with your vhost nginx file. Any \*.conf file in the ./container/nginx/sites/ directory will be read by nginx
4. add an entry in your hosts file that corresponds to the site created in step 3 (i.e. "127.0.0.1 docker.local")
5. run `docker-compose up --build` in the ./container directory

- mysql -u root -psecret -h 127.0.0.1 from host computer
- mysql -u root -psecret -h mysql from docker container (when setting up your web application the host is 'mysql' for the database container when accessed from the php docker container or the nginx container)
- ./container/scripts/ contains script files to connect to containers php and mysql
- your "web" directory from step 2 is the same as the /code directory in the php and nginx containers

### Prerequisites

- [Install docker-compose](https://docs.docker.com/compose/install/)

## Built With

- [Docker](https://docs.docker.com)
- [Nginx](https://docs.nginx.com)
- [MySQL](https://dev.mysql.com/doc/)
- [PHP-FPM](https://www.php.net/manual/en/install.fpm.php)

## Authors

- **url84t** - _Initial work_ - [url84t](https://github.com/url84t)

See also the list of [contributors](https://github.com/url84t/DEMP/contributors) who participated in this project.

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details
