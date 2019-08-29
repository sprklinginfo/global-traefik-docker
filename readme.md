# Running global Traefik container

Update the network names in *networks* section first. 

Run stand-alone traefik:
```
$ docker-compose -f traefik.yml up -d
```

## How to secure traefik web ui
Use [HTPASSWD Generate](http://www.htaccesstools.com/htpasswd-generator/) to create a username and password and add them to a .htpasswd file as shown below:
```
username:mypassword
```
or we can add to environment variables
```
HTTP_USERNAME=username
HTTP_PASSWORD=mypassword
```
In *docker-compose.yml* file for traefik container:
```
ports:
      - "80:80"
      - "443:443"
      - "XXXX:8080"
labels:
	- "traefik.enable=true"
	- "traefik.port=8080"
	- "traefik.frontend.auth.basic.users=${HTTP_USERNAME}:${HTTP_PASSWORD}"
```

```
$ openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout webapp.test.key -out webapp.test.crt
```
