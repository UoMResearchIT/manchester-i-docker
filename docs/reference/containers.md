# Overview of containers in Manchester-I #

## SWAG ##

* Input: incoming web traffic
* Output: outgoing web traffic
* Role: secure web connections, route requests to appropriate containers

SWAG is a container responsible for acquiring the certificates needed to secure web traffic and contains an NGINX reverse proxy for routing within the container network. It is the single point of access in the Manchester-i containerisation.

## mcri-frontend ##

* Input: web requests
* Output: Manchester-i graphical frontend
* Role: display Manchester-i platform, provide UI for user and sensor management, call backend API

The Manchester-i frontend provides the user experience for the Manchester-i platform, it creates and displays the graphics a user will see and makes API calls to the Manchester-i backend to retrieve the necessary data.

## mcri-backend ##

* Input: API calls from mcri-frontend
* Output: data from database connections
* Role: data retrieval and storage

The Manchester-i backend is responsible for retrieving and packaging data from both database instances when queried by the Manchester-i frontend.

## Mongodb ##

* Input: database queries
* Output: data
* Role: storing static data 

The Mongo database instance is responsible for storing data which does not change often, such as names and locations of sensors, usernames and passwords of user.

## Mongo express ##

* Input: web requests
* Output: data on web based UI
* Role: allowing administrators to inspect data stored in the Mongo database

Monogo express allows users to easily view, inspect and potential insert and edit data stored in the Mongo database.

## Influxdb ##

* Input: queries
* Output: data
* Role: storing time series data

The Influxdb database instance is responsible for storing data as it is retrieved from sensors from around the Manchester-i platform's registered sensors. 

## Chronograf ##

* Input: web requests
* Output: data visualisation
* Role: dashboard for Influxdb data

Chronograf provides a web based UI which users can use to define custom dashboards containing data stored in an Influxdb instance. In the Manchester-i containerisation it is used to allow administrators to view, inspect and diagnose problems with, sensors data.

## Data collectors ##

* Input: sensor brand
* Output: data pushed to Influxdb
* Role: execute API calls on sensors specified by the input, push output to storage

The data collection tools are triggered via a Galaxy workflow, they run API calls on sensors specified by the input and collect and persistently store the data in the Influxdb instance.

## Ofelia ##

* Input: specification of event timings
* Output: triggering of events
* Role: trigger the occurrence of regular events

Ofelia is a container which, though configuration supplied by Docker Compose, can be used to trigger regularly occurring events on other containers in the Docker Compose setup. In the Manchester-i containerisation it is used to trigger API calls to Galaxy, which trigger data gathering workflows.

## Galaxy ##

* Input: API calls, web UI
* Output: workflow execution, data storage
* Role: storage and execution of workflows

A containerised instance of Galaxy is used to provide the framework and implementation details for calling data harvesting workflows within this approach. 

## Galaxy API callers ##

* Input: Ofelia triggers
* Output: Galaxy API call
* Role: on Ofelia trigger, invoke Galaxy workflow

The Galaxy API caller is implemented using the BioBlend wrapper over the Galaxy API. It allows the Ofelia container to regularly invoke the data gathering events.
