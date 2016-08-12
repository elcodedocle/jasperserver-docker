

# A Jasperserver docker container.

## Installation/ Setup

* Copy the distro/bin folder to /srv/jasperserver on your docker host

* Edit the default.properties to meet your needs.

* Setup your environment.txt file in /srv/jasperserver/environment.txt

```
  SQLDB_TYPE=postgres
  SQLDB_HOST=localhost
  SQLDB_USERNAME=postgres
  SQLDB_PASSWORD=password
  SQLDB_PORT=5432
```

* Execute the run command going to a bash shell:

```
  docker run --rm -it \
    --hostname jasperserver \
    --name jaspserserver \
    --env-file=/srv/jasperserver/environment.txt \
    --volume=/srv/jasperserver/webapp:/var/lib/tomcat7/webapps \
    --volume=/srv/jasperserver/jasperreports-server-cp-5.6.1-bin:/data \
    --link postgis:postgis \
    --publish=8080:8080 \
    imatia/jasperserver \
    bash -l
```


* Run buildomatic js-install-ce.sh minimal.  Note the minimal install may 
  seem hung.  Be patient.  This has something to do with the java crypto
  libraries reading /dev/urandom on Linux and it hanging due to inadquate
  entropy to generate suitable randomness.


* Exit out of your docker container and then start it proper

```
  docker run \
    -it \
    --hostname jasperserver \
    --name jaspserserver \
    --env-file=/srv/jasperserver/environment.txt \
    --volume=/srv/jasperserver/webapp:/var/lib/tomcat7/webapps \
    --volume=/srv/jasperserver/jasperreports-server-cp-5.6.1-bin:/data \
    --publish=8080:8080 \
    imatia/jasperserver
```


