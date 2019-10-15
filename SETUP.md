### Setup Instructions
1. Checkout this repository to the local machine
2. Add the environment vars that are mentioned below in the ENVIRONMENT VARIABLES section. In Mac OS it would be at this path - `/usr/local/opt/apache2/bin/envvars`. If the path doesn't exist create the file.
3. Include the `dispatcher_module.conf` file in the `httpd.conf` file
   `Include <local-repo-path>/conf.d/dispacther_module.conf`
4. Check the configs using the `apachectl configtest`, it should return `Syntax OK`. If there are any errors or warnings resolve it 
5. Restart the apache to load the new configs

### ENVIRONMENT VARIABLES
_Use the env vars to better manage the configs for different environments._
> export RENDER_NAME=localhost
>
> export CACHE_DOCUMENT_ROOT=/usr/local/var/cache
>
> export LOG_LOCATION_ROOT=/usr/local/var/log/httpd
>
> export PUBLISH_DOMAIN_SERVER_NAME=aem-publish.local
>
> export AUTHOR_DOMAIN_SERVER_NAME=aem-author.local
>
> export CONFIG_ROOT_PATH=/Users/<path-to-the-local-repo>/aem-dispatcher

### Useful Commands 
###### apachectl tool commands
* apachectl start/stop/restart
* apachectl configtest

###### httpd service commands
* service httpd start/stop/restart
* service httpd configtest

###### Provide permissions to the cache or log directories 
* chown user:group directory
* chown user:group -R directory //Recursive operation

