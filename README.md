# Elastiflix

Elastiflix is a fictitious video streaming service company that provides a web-based user interface leveraging data from [The Internet Movie Database](https://tmdb.org/). Elastiflix provides a mechanism to query data from an indexed copy of TMDB data that sits in Elastic Cloud, allowing for high-performant, flexible management and querying of that data in order to provide an exceptional search experience.

## Pre-reqs

- [Elastic Cloud](https://cloud.elastic.co/) Deployment created, new accounts can sign-up for a limitless 14-day free trial to POC building a solution like this
- Docker Desktop Installed

### Setup Elastic Cloud

To get started with this sample, create a 14-day free trial of Elastic Cloud by going to https://cloud.elastic.co/registration and signing up with your Google or Microsoft Account or by signing up with another email. After logging in, you will be prompted with the Elastic Cloud console. Clicking `Create Deployment` will walk you through creating a new Elastic Cloud deployment, hosted in the Cloud Provider and region of your choice. You can run Elastic Cloud in Microsoft Azure, Google Cloud Platform or Amazon Web Services. If you expand settings you can choose your provider/region as well as other settings, which we can leave default for now. When you create `Create Deployment` Elastic Cloud will create all the necessary components to build the solution. There will be a username and password shown during the provisioning process, so be sure to save that somewhere safe as it is an admin account for your cluster.
<p align="center">
<img src="static/create-deployment.gif" height="500">
 </p>

Once the cluster is ready, you can navigate to it at the link provided. This will take you to Kibana, the solution management and visualization tool for Elastic. There are a few settings that you should capture and place in the sample to point it at this newly created Elastic Cloud instance. These settings are

- ELASTICSEARCH_PASSWORD: Password shown when deployment is created
- CLOUD_ID: URL Found on Deployments Page (Look for Cloud ID Area)
<p align="center">
<img src="static/get-cloud-id.gif" height="500">
</p>

- AS_BASE_URL & AS_SEARCH_API_KEY: URL of Elastic App Search Instance and API Key for search experience in the UI. Retrieve it like below

<p align="center">
<img src="static/loader/get_as_base_url.gif" height="500">
</p>

### Running the sample

This repository consists of 2 modules, that can be run as docker containers to show an End to End experience of ingesting, managing and searching with Elastic Cloud.

The modules are

- [Data Ingestion](/src/data-loader)
- [Search Experiences](/src/streaming-ui)


### What's next?

These 2 parts are just the start to building great search solutions, as Elastic also provides pre-built tools to help accelerate the building out of a top-notch search experience. You can find out more information about this at the [Elastic Enterprise Search](https://www.elastic.co/enterprise-search) section of the Elatic website.



# Elastiflix Website

React App preconfigured to query movies from Elastic Cloud deployment created in the [TMDB Loader Section](../data-loader/). The search experience is powered by [Search UI](https://github.com/elastic/search-ui), a free open source package written in React and Typescript to accelerate creating visual interfaces for search written and maintained by Elastic.

## Prerequisites


- [Data Import step completed](../data-loader)
- Docker Desktop Installed
- [Create and Setup Elastic CLoud](../../README.md#setup-elastic-cloud)
- Gather the below variables and place them in `env` file
    - AS_BASE_URL: URL of Elastic App Search Instance. Retrieve it like below
    - AS_SEARCH_API_KEY: Search only API Key. Retrieve it like below
   <img src="../../static/get-as-settings.gif" height="700">

    - ENGINE_NAME: LEAVE UNTOUCHED

## Build the docker image

```bash
docker build . -t elastiflix-ui:latest
docker run -d --env-file scripts/.env -p 5000:80 elastiflix-ui
```

if you get an error similar to `The engine "node" is incompatible with this module.`, try pulling the latest version of `docker pull node:12` or run the docker build command with the additional flag to disable caching: `docker build . --no-cache -t elastiflix-ui:latest`

## Run App

Open browser to https://localhost:5000 to see the UI in action!
   <img src="../../static/ui/ui.png" height="700">
