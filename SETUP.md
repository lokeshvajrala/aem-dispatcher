### Setup Instructions
1. Checkout this repository to the local machine
2. Add the environment vars that are mentioned in the ENVIRONMENT VARIABLES section. In Mac OS it would be at this path - `/etc/apache2/bin/envvars`. 
3. Include the `dispatcher_module.conf` file in the `httpd.conf` file. In Mac OS the `httpd.conf` location would be at `/etc/apache2/httpd.conf`
   `Include <local-repo-path>/conf.d/dispacther_module.conf`
4. Test the configs using the `apachectl configtest`, it should return `Syntax OK`. If there are any errors or warnings resolve it 
5. Restart the apache to load the new configs `apachectl restart`

### ENVIRONMENT VARIABLES
_Use the env vars to better manage the config paths._
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

### Vhsots
_Add the host entries in the `/etc/hosts` file_ 
> 127.0.0.1      aem-author.local
>
> 127.0.0.1      aem-publish.local

### AEM Servers for this setup
> author - localhost:4502
>
> publish1 - localhost:4503
>
> publish2 - localhost:5503

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

