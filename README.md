# WANdisco Fusion 

## Overview
This repository contains a Docker Compose stack which deploys the WANdisco Fusion platform and provides a fully functional evaluation version to support live migration between Hadoop (CDH, HDP, ASF) and Cloud storage (S3, ADLS). The stack is designed for standalone operation in two zones or as a single zone to connect with another Fusion server. 

The ./setup-env.sh script lets you choose the desired platform and configure storage settings before running docker-compose up -d. 

## Prerequisites 
1. [Docker](https://docs.docker.com/install/overview/) and [Docker Compose](https://docs.docker.com/compose/install/) installed on a suitable host
1. Storage Details for either a Hortonworks HDP 2.6.5 Cluster, a CDH 5.13 Cluster, an Azure ADLS Gen 1 or Gen 2 account - Any of which Fusion can move data between.

## Installation Process
There are a series of steps that must be completed in order to properly deploy and leverage WANdisco Fusion:

1. [Download](https://github.com/WANdisco/fusion-docker-compose/archive/master.zip) and unzip or git clone the configuration files. 

1. Run `./setup-env.sh` and follow the prompts

1. Start the cluster(s) with:

```bash
docker-compose up -d
```

### Modifying The Configuration
Configuration can be changed in the following files:

- common.env
- zone_a.env
- zone_b.env (when a second zone has been configured)

If you make changes to these files, run `./setup-env.sh` and they will be applied to the docker compose files.

## Usage
To interact with the Docker Compose stack, ensure you are in the same directory as the `docker-compose.yml`. 

Then, to deploy the containers:
```bash
docker-compose up -d
```

To bring down the containers:
```bash
docker-compose down
```

To view the status of the deployed containers and port allocations:
```bash
docker-compose ps
```
</br>

> Note: The Docker managed volumes persist between container restarts. This ensures that any configuration and database changes are kept once you get up and running. You can remove them if you want to wipe out changes made _after_ initial launch, resetting the volumes. To remove them specify the `-v` flag to `docker-compose down`. 

### UI Access 
Fusion UI is available at http://docker_host:8083 for First Zone and http://docker_host:8583 for Second Zone, with username and password admin/admin.


### Ensure The Proper License Is Being Used
Am evaluation license is provided by default. The license is fully functional but has limited data transfer capacity. It can be extended or upgraded by contacting WANdisco sales - sales@wandisco.com.

If you wish to apply an updated license add the following line to common.env and run setup-env.sh -u to apply the license to the docker compose files, then docker-compose restart:

common.env
```LICENSE_FILE=./path/to/license.key ```

## License
This repository is Apache 2.0 licensed. Please see `./LICENSE` for more information.

Images provided through Dockerhub are offered for evaluation purposes. By pulling these images, you agree you have read, understood and accept the [WANdisco EULA](https://www.wandisco.com/eula).

Contact sales@wandisco.com for other distros and licensing. 
