## Building from source

::: warning
Notice! All example commands below are tested with Debian 10. If you are using a different operating system you need to understand what happens in these commands and translate them to work on your operating system! 
We are not responsible for any damages to your system!
Think before you execute any command shown on this page!

:::

### Picking a Server OS

upowdb runs on a wide range of operating systems, just pick what you like.

| Operating System | Version |     Supported      | Note                    |
| ---------------- | ------- | :----------------: | ----------------------- |
| **Debian**       | 10      | :white_check_mark: | tested, **recommended** |

### Dependencies

* A webserver (Apache, NGINX, etc.)
* `git`
* `yarn`

#### Example Dependency Installation
The following commands should present an example on how to install the needed dependencies. 
If you are using a different operating system you need to use your operating system's package manager and determine the needed packages yourself.

``` bash
# Install Dependencies
apt -y install nginx git curl gnupg
# Install yarn - configure yarn repository
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list
# Install yarn
apt update && apt -y install yarn
```

### Clone GIT Repository

The first step in the build process is to clone the GIT Repository.
Below is an example on how to perform this task.

``` bash
git clone --recursive https://git.scc.kit.edu/pse-lernplattform-datenbanken/frontend.git upowdb-frontend
```

### Installation

#### Generate application files

Change to your newly created folder and use yarn to install all needed dependencies, after that you can build the application.

``` bash
cd upowdb-frontend
yarn install
yarn build
```

#### Copy files to be served by your webserver
The application files were copied to the `dist` folder when you ran the `yarn build` command above. Now we need to but the files inside the folder which is delivered by our webserver.

``` bash
cp -r dist/ /var/www/upowdb
```

#### Configure webserver to serve our application
Now that we generated all needed files and copied them to the correct folder we need to configure our webserver to serve them.

Below is an example how your nginx.conf could look like. If you are serving multiple pages with your webserver you should already know how to setup your webserver. Just remember to include the settings shown [here](https://router.vuejs.org/guide/essentials/history-mode.html#example-server-configurations).

``` bash
#/etc/nginx/nginx.conf
user  www-data;
worker_processes  auto;
error_log  /var/log/nginx/error.log warn;
pid        /run/nginx.pid;
events {
  worker_connections  1024;
}
http {
  include       /etc/nginx/mime.types;
  default_type  application/octet-stream;
  log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                    '$status $body_bytes_sent "$http_referer" '
                    '"$http_user_agent" "$http_x_forwarded_for"';
  access_log  /var/log/nginx/access.log  main;
  sendfile        on;
  keepalive_timeout  65;
  server {
    listen       80;
    server_name  localhost;
    location / {
      root   /var/www/upowdb;
      index  index.html;
      try_files $uri $uri/ /index.html;
    }
    error_page   500 502 503 504  /50x.html;
    location = /50x.html {
      root   /usr/share/nginx/html;
    }
  }
}
```

#### Set Permissions
The last step in the installation process is to set the correct permissions for the application files so the webserver can use them properly.

``` bash
# If using NGINX or Apache:
chown -R www-data:www-data /var/www/upowdb
```

## Using the pre-generated container image

A ready to use container image including the frontend application is available at:

https://cloud.docker.com/u/upowdb/repository/docker/upowdb/frontend

### Dependencies

- curl
- docker

#### Example Dependency Installation

The following commands should present an example on how to install the needed dependencies. 
If you are using a different operating system you need to use your operating system's package manager and determine the needed packages yourself.

```bash
# Install Dependency
apt -y install curl

# Download and install Docker CE
curl -sSL https://get.docker.com/ | CHANNEL=stable bash
```

#### Start Docker on Boot

To make sure that Docker is started when you boot your machine run the following command (For operating systems with systemd).

```bash
systemctl enable docker
```

### Start the frontend container

::: warning
It is within your responsibility to secure the access to this container (e.g. using a reverse proxy like Traefik).
Don't forget to configure SSL.

:::

```bash
docker run --rm -d -p 80:80 docker.io/upowdb/frontend
```