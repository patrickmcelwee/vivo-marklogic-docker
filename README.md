Docker for VIVO
---------------

This project contains code for dockerizing [VIVO](http://vivoweb.org).

In particular, it supports creating the following containers:

* app:  Compiles and deploys the VIVO application.
* db:  Instantiates a MySQL db.
* tomcat:  Instantiates an instance of Tomcat for the app to run in.
* load:  Provides an environment for loading VIVO.

Building images
===============
Each container provides a script named `build.sh` to build an image.

Running containers
==================
Each container provides a script named `container.sh` to instantiate a container.

Containers should be instantiated in the following order: app, db, tomcat, load.

Container-specific notes
========================

### app container:

* Before instantiating the db container, wait for the app container to complete
compiling and deploying the VIVO application. Once completed, the app container
will stop running.  (Thus, while running it is listed by `docker ps`. Once
completed, it is only listed by `docker ps -a`).

### tomcat app:

* Complete control is available over VIVO's runtime properties.  At the very
least, your domain must be provided in `container.sh`.  Additional runtime
properties can be overridden by providing as environment variables.  See
tomcat/prop_util/prop_util.py.
* Starting up the VIVO application in Tomcat takes a long time.  As in several
excruciating minutes.
* Once the VIVO application is running, you will be required to change the root
password.  The default username is "vivo_root@yourinstitution.edu" and password is "rootPassword".
* VIVO performs a series of smoke tests when starting up.  You may be warned if
SMTP is not available for sending email.

### load app:

* The load app includes an instance of Apache to support a SPARQL load.
* The load app shares a local directory with the container.  This is intended to contain
the load code and can be specified in `container.sh`.
* To use the load app to execute load code, create a bash shell with `docker exec -it vivo_load /bin/bash`.