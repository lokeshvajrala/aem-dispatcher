### Sling Dynamic Include Setup Instructions
1. Download and Install the latest Sling Dynamic Include bundle - https://github.com/apache/sling-org-apache-sling-dynamic-include/releases
2. Configure the Sling Dynamic Include via OSGi Configuration Manager -   http://localhost:4503/system/console/configMgr/org.apache.sling.dynamicinclude.Configuration
3. Update Apache HTTPD Web server's httpd.conf file to enable the Include Module.
4. Update the vhost file to respect include directives.
5. Update the dispatcher.any configuration file to support (1) nocache selectors and (2) enable TTL support.
   
   ``` add deny caching rule in the cache rules 
   /0006 {
       /glob "*.nocache.html*"
       /type "deny"
   }

   ```
7. Restart Apache `apachectl restart`
