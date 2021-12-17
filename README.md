Python Logging
==============

This is a Docker (with docker-compose) environment for Python Logging (AWS Opensearch and CloudWatch)

![Python Logging Graph](./docs/python-logging.png?raw=true "Python Logging Graph")

# Installation

1. First, clone this repository:

```bash
$ git clone https://github.com/nietzscheson/python-logging
```
2. Copy the environment vars and set the AWS credentials:

```bash
$ cp .env.dist .env
```
3. Init project
```bash
$ make
```
4. Show containers:
```bash
$ make ps
```
This results in the following running containers:
```bash
> $ docker-compose ps
        Name                       Command               State                                 Ports
-----------------------------------------------------------------------------------------------------------------------------------
opensearch              ./opensearch-docker-entryp ...   Up      0.0.0.0:9200->9200/tcp, 9300/tcp, 0.0.0.0:9600->9600/tcp, 9650/tcp
opensearch-dashboards   ./opensearch-dashboards-do ...   Up      0.0.0.0:5601->5601/tcp
py                      python3                          Up
```
5. Before inserting data into Opensearch, make sure it is working by going to https://localhost:5601:

6. To shipping logs in Opensearch (In order to look at the data, you must create an index (with opensearch) and then a dashboard in the Discover tab):
```bash
$ make ingest.opensearch
```

![Opensearch Logs](./docs/opensearch.png?raw=true "Opensearch Logs")

7. To shipping logs in AWS CloudWatch:
```bash
$ make ingest.cloudwatch
```

![Cloudwatch Logs](./docs/cloudwatch.png?raw=true "Cloudwatch Logs")

## References

- https://docs.python.org/3/library/logging.html
- https://www.elastic.co/guide/en/cloud/current/ec-getting-started-search-use-cases-python-logs.html
- https://coralogix.com/blog/python-logging-best-practices-tips/