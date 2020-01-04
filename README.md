# Couchmovies Demo

This code demonstrates Data Storage, the Admin UI, N1QL queries, Full Text Search features and real-time Analytics in Couchbase.

This repo contains:

* A demo script
* A prelude Powerpoint presentation
* A docker compose file
* A pre-built Tableau dashboard

The code to build the docker containers used in this demo may be found [here](https://github.com/escapedcanadian/couchmovies).

Honorable mention goes to [Denis Rosa](email:denis.rosa@couchbase.com) for building the [intial version of the FTS app](https://github.com/deniswsrosa/couchflix).  Thanks Denis!

##Prerequisites
To demo Couchbase, N1QL and FTS

* Docker installed on your laptop (this has only been tested on Mac)
* An internet connection (used only to retrieve movie poster images from TMDB - this restriction may be lifted in the future)

The Analytics portion of the demo also requires:

* CDATA ODBC Connector for Couchbase - licenesed, installed and configured (see instructions below)
* Tableau Desktop - licensed and installed

## Running the Demo
Clone this repo onto your laptop.

Unzip and read CouchmoviesDemoScript.  It also contains speaker's notes for the CouchmoviesPrologue Powerpoint presentation, should you choose to use it.

### Starting the environment
This demo uses docker compose to create a network of multiple Docker containers.

* A single node Couchbase 'cluster'
* A RESTful service that fronts the database, writting in Java and Spring (exposed on port 8080)
* A simple http server that serves up a single page web application (exposed on port 8000)
 * in the future, this web server may also supply the minimal number of movie posters required

To create the environment, change to the directory that contains the repo (and the docker-compose.yaml file). Run the following ...
```
docker-compose run -d web
```

Please allow a full minute for the environment to start.

### Shutting down the environment
From the directory that contains the docker-compose.yaml file, run ...

```
docker-compose down
```
Close Tableau if it is running.