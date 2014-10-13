Mule ESB Management Console Docker Image
===============

This project contains a Dockerfile for the deployment and packaging of a Mule ESB Management Console with Docker.

Preparing the Docker base image
---------------

Due to restrictions of the Enterprise version, the Docker image needs to be set up for individual usage beforehand. It is required to provide the Enterprise standalone server from Mulesoft. In this Dockerfile we asume the downloaded trial version from [mulesoft.com](http://www.mulesoft.com/mule-esb-enterprise-30-day-trial), located in the same folder as the Dockerfile.

Hence the directory should look like this:
* mule-mmc/
* mule-mmc/Dockerfile
* mule-mmc/mmc-distribution-mule-console-bundle-3.5.1.zip

Building and tag the Docker base image
---------------

```bash
docker build --tag="mule-mmc" .
```

Starting the Mule ESB Management Console instance
---------------

Start a Mule MMC instance

```bash
docker run -t -i -p 8585:8585 --name='mule-mmc-node' mule-mmc
```

> Notice: On OSX boot2docker VBox requires port forwarding from docker -> VBox -> host
>
> ```bash
>  boot2docker ssh -L 8585:localhost:8585
> ```