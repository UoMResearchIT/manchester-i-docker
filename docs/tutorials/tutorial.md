# Deploying an instance of Manchester-I #

This tutorial will take you through the steps needed to create your own locally hosted instance of Manchester-I. 

The tutorial will assume the use of a Linux system but should be compatible with Windows / WSL / Mac environments with standard modifications to the terminal commands.

The tutorial will walk you through the process of obtaining a URL from [DuckDNS](https://www.duckdns.org/) so users may trial this deployment for free. If you have or can acquire a full URL please feel free to omit this step and use your own URL.

The steps will be as follows:
* [Downloading the Manchester-I template](#downloading-the-template)
* [Configuring the Manchester-I template](#configuring-the-template)
* [Running Manchester-I](#running-manchester-i)

## Prerequisites ##

_n.b. The full installation of prerequisite software is beyond the scope of this tutorial_

To deploy Manchester-I using this approach, the following software and setup is required:
* [Docker Engine](https://docs.docker.com/engine/install/)
* [Docker Compose](https://docs.docker.com/compose/install/)
* [Docker post installation steps](https://docs.docker.com/engine/install/linux-postinstall/)

## Downloading the template ##

To deploy an instance of Manchester-I, the docker-compose file (and supporting configuration) which describes the components of the service, and how they are connected, must be obtained. This is achieved by cloning this GitHub repository:

```console
$ git clone https://github.com/UoMResearchIT/manchester-i-docker.git
$ cd manchester-i-docker
```

With the source code obtained, the template environment should be copied and renamed to '.env':

```console
$ cp .env.template .env
```

## Configuring the template ##

The environment file can be edited with any text editor, e.g. nano is suitable:

```console
$ nano .env 
```

In the '.env' file, several variables are found, these should be changed. Some suggestions are made below:

* MONGO_USER: A username for the Mongo user, user's choice, preferably hard to guess (string)
* MONGO_PASS: A password for the Mongo user, user's choice, preferably randomly genearted (string)
* INFLUX_HOST: For most users, should not be changed 
* INFLUX_PORT: For most users, should not be changed 
* INFLUX_DB_NAME: For most users, should not be changed 
* INFLUX_USER: A username for the Influx user, user's choice, preferably hard to guess (string)
* INFLUX_PASS: A password for the Influx user, user's choice, preferably randomly genearted (string)
* URL: The URL the Manchester-I image should be hosted at (string)*
\* See the next section for details on how to acquire a URL from DuckDNS if desired

### DuckDNS ###

DuckDNS is a service which allows users for register a subdomain on their URL, functioning as a public DNS. 

If you wish to use this service to obtain a URL for testing Manchester-I, first login to [DuckDNS](https://www.duckdns.org/).

Once logged in, make a note of the "token" field displayed to you. This (verbatim) lshould be used to populate the DUCKDNS_TOKEN variable in the '.env' file.

Next, create a subdomain using the "add domain" field and button. Populate the URL variable in the '.env' file with the full URL you have created.

## Running Manchester-I ##

With the configuration file fully populated, it is time to launch the Manchester-I instance.

This is achieved using docker-compose with the following command:

```console
$ docker-compose up
```

The service should now be up and running.
