### Permission Sensitive Caching Setup Instructions
1. Create the Authorization Servlet and deploy it to AEM. Example Servlet

```
package com.adobe.support.security.dispatcher;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;
import org.apache.felix.scr.annotations.Property;

import org.apache.sling.api.SlingHttpServletRequest;
import org.apache.sling.api.SlingHttpServletResponse;
import org.apache.sling.api.servlets.SlingSafeMethodsServlet;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import javax.jcr.Session;

@Component
@Service
@Property(name="sling.servlet.paths", value= {"/bin/permissioncheck"})
public class PermissionHeadServlet extends SlingSafeMethodsServlet {
    private static final Logger log = LoggerFactory.getLogger(PermissionHeadServlet.class);
    
    public void doHead(SlingHttpServletRequest request, SlingHttpServletResponse response) {
        try { 
            //retrieve the requested URL
            String uri = request.getParameter("uri");
            //obtain the session from the request
            Session session = request.getResourceResolver().adaptTo(javax.jcr.Session.class);     
            //perform the permissions check
            try {
                session.checkPermission(uri, Session.ACTION_READ);
                log.info("authchecker says OK");
                response.setStatus(SlingHttpServletResponse.SC_OK);
            } catch(Exception e) {
                log.info("authchecker says READ access DENIED!");
                response.setStatus(SlingHttpServletResponse.SC_FORBIDDEN);
            }
        }catch(Exception e){
            log.error("authchecker servlet exception: " + e.getMessage());
        }
    }
}

```

2. Configure Dispatcher for permission-sensitive caching. Add the `auth_checker` section to the dispatcher.any file and restart the apache. 
   The example auth_checker configuration - `/conf/publish/auth_checker.any`
