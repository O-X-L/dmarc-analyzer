# DMARC Analyzer

This dockerized stack is mainly utilizing the [parsedmarc](https://github.com/domainaware/parsedmarc) project.

## Stack

* [parsedmarc](https://github.com/domainaware/parsedmarc) to parse DMARC reports
* [OpenSearch](https://opensearch.org/) to store data
* [Grafana](https://grafana.com/) to visualize data

----

## Prerequisites

* Create a mailbox as target for the DMARC reports
* Configure your [SPF](https://www.cloudflare.com/learning/dns/dns-records/dns-spf-record/), [DKIM](https://www.cloudflare.com/learning/dns/dns-records/dns-dkim-record/) & [DMARC](https://www.cloudflare.com/learning/dns/dns-records/dns-dmarc-record/) DNS-records

  * DMARC: `TXT _dmarc.<DOMAIN>.<TLD>`

    Test Example: `v=DMARC1; p=none; rua=mailto:dmarc@oxl.at; ruf=mailto:dmarc@oxl.at; sp=none; adkim=s; aspf=s; fo=1;`

    Active Example: `v=DMARC1; p=quarantine; rua=mailto:dmarc@oxl.at; ruf=mailto:dmarc@oxl.at; sp=quarantine; adkim=s; aspf=s; fo=1;`

----

## Usage

* Change the data owner UID inside the `Dockerfile_opensearch` and `docker-compose.yml` if needed
* Create the data directory and change its owner:

  ```bash
  mkdir -p ./data/
  chown ${OWNER}:${OWNER} ./data
  ```

* Change options inside the `docker-compose.yml` as needed
* Configure settings inside the `parsedmarc.ini` as needed

* Start: `docker compose -f docker-compose.yml up`
* Check for error logs - you may have configuration issues
* Access the web interface: [http://localhost:3000](http://localhost:3000)

----

## Documentation

* [Configuration file](https://domainaware.github.io/parsedmarc/usage.html#configuration-file)
