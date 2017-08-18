# Docker-Environment
Local hosting with [Docker](https://www.docker.com/) environment with [NGINX](https://hub.docker.com/_/nginx/), [PHP](https://hub.docker.com/r/nicoorfi/php/), [MySQL](https://hub.docker.com/_/mysql/).

#### Default MySQL credentials
````
 root_password = root 
 user = db
 db_password= db
 ````
 
 ## Basics
 * Shared projects folder should be located at `home/$USER/Projects` else you have to edit `docker-compose.yml` to set your projects path within the `nginx` section. 
 * Use `dmesg | docker inspect nginx | egrep '"IPAddress": "172\.[0-9]{1,3}\.[0-9]{1,2}\.[0-9]"'` to get your docker ip address and then add it to your hosts.
 * A `home/$USER/Projects/html` folder is needed in order `php-app` to start correnctly.
 * If you want to avoid typing `sudo` whenever you run the `docker` command, add your username to the `docker` group:  `sudo usermod -aG docker ${USER}`. 
 ### Hosts
 * On Linux/Mac `sudo vim /etc/hosts` 
 * If you are on Windows, you can find instructions for altering your hosts file [here](http://www.thewindowsclub.com/hosts-file-in-windows).
 * On Linux use `sudo sysctl -w vm.max_map_count=262144` to give to the elastic search container enought memory to start. To make this change permanent you have to add `vm.max_map_count=262144` to your `/etc/sysctl.conf` as root.

 Your hosts file on Linux should look like this
 ````
#<ip-address>	<hostname.domain.org>	<hostname>
0.0.0.0		localhost.localdomain	localhost
10.5.0.4      example.com
10.5.0.5      example.com
10.5.0.6      example.com
10.5.0.7      example.com
::1		localhost.localdomain	localhost
 ````
 
### Elastic Search 
* Version: 1.7.3 
 
### PHP
* Version: 7.1.6

### MySQL
* Version: 5.7.18

### NGINX
* Version: 1.12.0 
* `/etc/nginx` is linked with the `./nginx` folder so any change configurations are done in the `./nginx` folder.
