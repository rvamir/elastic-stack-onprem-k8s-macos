# Elastic Stack on-prem with Helm on macOS

# Setting up the Elastic Stack on macOS using Docker Compose

This guide covers deploying Elasticsearch and Kibana locally on macOS using Docker Compose for a persistent and easy-to-manage Elastic Stack setup.

## Overview

- Deploy Elasticsearch and Kibana directly using Docker containers.
- Use Docker Compose to simplify startup, shutdown, and persistent data handling.
- Enables quick redeployment without losing data.
- Optionally, if local setup is difficult, you can use the [Elastic Cloud free trial](https://cloud.elastic.co).

## Prerequisites

- Docker Desktop installed and running on macOS
- Basic Docker and command-line knowledge
- `curl` or similar HTTP client for API testing

## Steps to Setup

1. **Clone or download this repository.**

2. **Start the stack:**

docker-compose up -d
Verify Elasticsearch is running by sending an API request:

curl http://localhost:9200
You should receive a JSON response with cluster info.

Access Kibana UI:

Open http://localhost:5601 in your web browser.

Persistence
Docker volumes are configured in docker-compose.yml to ensure Elasticsearch and Kibana data persist across restarts.
volume elastic-stack-onprem-k8s-macos_es_data is a Docker-managed persistent volume.
Data inside /usr/share/elasticsearch/data within the container is stored persistently in the named Docker volume.
The volume physically lives inside Docker Desktop’s VM, but it keeps your data safe across container restarts.

Monitoring Resource Usage
To determine the CPU and memory consumption of the Elastic applications, use the following command:


docker stats

Example output:
CONTAINER ID   NAME          CPU %     MEM USAGE / LIMIT     MEM %     NET I/O           BLOCK I/O        PIDS
25d573f9bfca   kibana        2.34%     619.1MiB / 7.654GiB   7.90%     5.43MB / 30.9MB   288MB / 4.1kB    12
976ddaec5833   elasticsearch 3.18%     4.428GiB / 7.654GiB   57.86%    25.9MB / 4.94MB  
 
Alternatively, system tools like:
macOS Activity Monitor top in Terminal


Troubleshooting & Notes
The version attribute in docker-compose.yml is deprecated and has been removed to avoid warnings.

Ensure Docker Desktop has sufficient RAM allocated (recommend at least 8GB) for Elasticsearch to run smoothly.

Elasticsearch requires enough memory; otherwise, it may fail to start or perform poorly.
