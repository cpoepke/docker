Standalone Mule ESB Enterprise Docker Image
===============

This project contains a Dockerfile for the deployment and packaging of a standalone Mule ESB Enterprise with Docker.

Preparing the Docker base image
---------------

Due to restrictions of the Enterprise version, the Docker image needs to be set up for individual usage beforehand. It is required to:
- provide the Enterprise standalone server from Mulesoft. In this Dockerfile we asume the downloaded trial version from [mulesoft.com](http://www.mulesoft.com/mule-esb-enterprise-30-day-trial), located in the same folder as the Dockerfile.
- provide the Enterprise license file from Mulesoft, located in the same folder as the Dockerfile.

Hence the directory should look like this:
* mule-ee/
* mule-ee/Dockerfile
* mule-ee/mmc-distribution-mule-console-bundle-3.5.1.zip
* mule-ee/mule-ee-license.lic

Building and tag the Docker base image
---------------

```bash
docker build --tag="mule-ee" .
```

Container types
---------------

There are two way now to use the Docker images, depending on the overall scenario:
- you can use the base images to startup and create in a classical operations sense multiple standalone Mule ESB instances and one MMC instance. These can be used as a cluster as usual with hot deployment over MMC etc.
- or, which we recommend, create an Docker image for each Mule ESB application to isolate applications from each other and this way startup and create multiple standalone Mule ESB instances and one MMC instance. This might be a an option in a Micro Services or SOA scenario.

Standalone Mule ESB Enterprise Container
---------------

Start a standalone Mule ESB Enterprise instance

```bash
docker run -t -i --name='mule-ee-nodeX' mule-ee
```

> Notice: On OSX boot2docker VBox requires port forwarding from docker -> VBox -> host
>
> ```bash
>  boot2docker ssh -L 8585:localhost:8585
> ```

App specific container image
---------------

```bash
FROM                    mule-ee:latest
.
.
ADD                     mule-app/target/mule-app-1.0.0-SNAPSHOT.zip /opt/mule-standalone-3.5.1/apps/
```

Build application specific Docker image:

```bash
docker build --tag="my-mule-app-image" .
```

Start app specific image:

```bash
docker run -t -i --name='mule-app-node' my-mule-app-image
```