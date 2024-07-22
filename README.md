# EDS (Ensemble Defense System- Hybrid based IDS with SIEM)

we design, develop, and evaluate a novel Ensemble Defense System (EDS), addressing the critical need for advanced defense systems. The EDS combines the capabilities of Intrusion Detection Systems (IDS) and Security Information and Event Management (SIEM) to provide an effective defense against cyber threats. The EDS incorporates hybrid-based IDS technologies, leveraging the strengths of signature-based IDS tools like Zeek and Suricata and behavioral-based IDS tools like Slips. By utilizing hybrid-based IDS, the EDS provides a more effective system for countering cyber threats. Moreover, the EDS integrates open-source SIEM, specifically Elasticsearch, to provide data management and analysis capabilities and create user-friendly visualization.

Steps to evaluate EDS:

Pull the file from this repositiory and unzip it. I have tested ubuntu but free feel to test it in other environment as we will be running docker containers.

cd eds -> cd EDS

nano .env -> change the contents of the environment file according to your needs.

# now after proper configurations are done, we will start the containers one by one.

ES
==
docker-compose up -d elasticsearch
docker logs -f eds-elasticsearch-1

curl -X POST --user elastic:changeme 0.0.0.0:9200/_security/service/elastic/kibana/credential/token/token1?pretty

add the generated key in nano docker-compose.yml in kibana section

Kibana
======

docker-compose up -d kibana
docker logs -f eds-kibana-1

filebeat
========
docker-compose build --no-cache filebeat
docker-compose up -d filebeat
docker logs -f eds-filebeat-1

zeek
====
docker-compose build --no-cache zeek
docker-compose up -d zeek
docker logs -f eds-zeek-1

suricata
========
docker-compose build --no-cache suricata
docker-compose up -d suricata
docker logs -f eds-suricata-1

slips
=====
docker-compose build --no-cache slips
docker-compose up -d slips
docker logs -f eds-slips-1


##Note
I have added custom rules for DOS attack, SQL injection and privilge escaltion in the suricata folder. Make your own rules for custom attack detection.
