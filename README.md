# Couchmovies Demo

This code demonstrates Data Storage, the Admin UI, N1QL queries, Full Text Search features and real-time Analytics in Couchbase.

This repo contains:

* A demo script
* A prelude Powerpoint presentation
* A docker compose file
* A pre-built Tableau dashboard

Pre-built docker images used for the demo, as referenced by the docker compose file, should already exist.  If you wish to rebuild/modify them, the code to build the docker containers used in this demo may be found [here](https://github.com/escapedcanadian/couchmovies).

Honorable mention goes to [Denis Rosa](email:denis.rosa@couchbase.com) for building the [intial version of the FTS app](https://github.com/deniswsrosa/couchflix).  Thanks Denis!

## Prerequisites (designed for Mac laptop)
To demo Couchbase, N1QL and FTS

* Docker installed on your laptop 

 [https://hub.docker.com/?overlay=onboarding](https://hub.docker.com/?overlay=onboarding)

* jq installed on your laptop (pretty-prints and filters json results)

 ``` brew install jq ```

* Git installed on your laptop 

 ```brew install git```

* Clone this repo 

 ```git clone https://github.com/escapedcanadian/couchmovies-demo <demoDir>``` 
 
* Pull the requied Docker images 

 ```<demoDir>/docker-compose pull```

* *Optional* - During the demo, an internet connection is only used to retrieve movie poster images from TMDB. ***If you follow the script exactly***, all the the required movie posters are already available without an internet connection.  If you choose to go 'off script' and search for different movies, you will require a live internet connection.

### Analytics prerequisites
The bulk of the demo (N1QL & FTS) do not have any dependencies on these components.  You can omit installing these components if you do not want/need the analytics element of the demo.

The Analytics portion of the demo also requires:

* ODBC Manager (if you are on a mac)
* CDATA ODBC Connector for Couchbase - licensed, installed and configured (see instructions below)
* Tableau Desktop - licensed and installed

#### Install ODBC Manager (on Mac)
For mac laptops, you will need an ODBC manager. There are many available, but a decent one is [here](http://www.odbcmanager.net/).


#### Installing CDATA
Instructions for licensing and installing CDATA may be found [here](https://docs.google.com/document/d/13EW5Ksf6mfHS1nDxjK5fqwFYNTtcabpGPUkMnpOgO24).

#### Configuring the ODBC Entry
1. Open ODBC Manager.
2. Select System DSN from the top menu
3. Press 'Add...'
4. Select CData ODBC Driver for Couchbase
5. Set the ***Data Source Name (DSN):*** to ***Couchmovies Demo***
6. For each of the following, press ***Add*** in the bottom right of the screen to set the ***Keyword:Value*** pairs
 * Server : ***127.0.0.1***
 * CouchbaseService:  ***Analytics***
 * User: ***Administrator***
 * Password: ***password***
 * verbosity: ***5***
 * logfile: ***/Users/<mac username>/cdata.log***
 * Username: ***Administrator***
 * Port: ***8095***

#### Installing Tableau
* Download from [here](https://www.tableau.com/products/desktop/download)
* License using the following code, which is for our use only, as their partner:  ***TCFT-4E52-1B80-9423-04F2***
*

 Remember to be kind to their BDRs when start emailing you five minutes after you download.

## Running the Demo

Unzip and read CouchmoviesDemoScript.  It also contains speaker's notes for the CouchmoviesPrologue Powerpoint presentation, should you choose to use it.

OPTIONAL: If you want to enable the image cover (the image that appears when you click over a movie) you will need to install a chrome driver:

```
brew cask install chromedriver //on mac
```

### Starting the environment
This demo uses docker compose to create a network of multiple Docker containers.

* A single node Couchbase 'cluster' (exposed to localhost using default Couchbase ports)
* A RESTful service that fronts the database, writting in Java and Spring (exposed to localhost on port 8080)
* A simple http server that serves up a single page web application (exposed to localhost on port 8000)
 * This web server also supplies the movie poster images *when you follow the script exactly*

To create the environment, change to the directory that contains the repo (and the docker-compose.yml file). Run the following ...

```
docker-compose run -d
```

Please allow a full minute for the environment to start.

### Running the tweet feeder
When called for in the script, you can start the tweet feeder with the following command (run from the same demo dir)...

```
docker-compose exec couchabse startFeeder
```

You shouldn't need to, but if you want to reset the ```tweettarget``` bucket in order to run the analytics demo again, without restarting the environment, you can run

```
docker-compose exec couchbase resetTweets
```

### Shutting down the environment
From the directory that contains the docker-compose.yaml file, run ...

```
docker-compose down
```
Close Tableau if it is running.