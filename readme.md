keycloak setup

add proxy-address-forwarding
<subsystem xmlns="urn:jboss:domain:undertow:12.0">
   <buffer-cache name="default"/>
   <server name="default-server">
      <ajp-listener name="ajp" socket-binding="ajp"/>
      <http-listener name="default" socket-binding="http" redirect-socket="https"
          proxy-address-forwarding="true"/>
      ...
   </server>
   ...
</subsystem>

configure nginx to forward request information
proxy_set_header X-Forwarded-For $proxy_protocol_addr; # To forward the original client's IP address 
proxy_set_header X-Forwarded-Proto $scheme; # to forward the  original protocol (HTTP or HTTPS)
proxy_set_header Host $host; # to forward the original host requested by the client

create realm
create user / credential

docker run -it --rm -p "80:80" -v "$(pwd)/vuejs:/usr/share/nginx/html" -v "$(pwd)/nginx/nginx.conf:/etc/nginx/nginx.conf:ro" nginx