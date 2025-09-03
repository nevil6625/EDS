# 🛡️ Ensemble Defense System (EDS) – Hybrid IDS with SIEM

The **Ensemble Defense System (EDS)** is a hybrid security framework that integrates multiple Intrusion Detection Systems (IDS) with a Security Information and Event Management (SIEM) solution.  

The goal is to provide a stronger and more efficient defense against cyber threats by combining:  
- 🔹 **Signature-based IDS** tools such as **Zeek** and **Suricata**  
- 🔹 **Behavior-based IDS** tools such as **Slips**  
- 🔹 **Open-source SIEM** (**Elasticsearch & Kibana**) for log management, analysis, and visualization  

This hybrid approach leverages the strengths of each system to achieve:  
✅ Improved detection accuracy  
✅ Reduced false positives  
✅ Stronger resilience against evolving threats  

---

## ⚙️ Steps to Evaluate EDS  

Clone this repository and unzip the files.  
Tested on **Ubuntu**, but feel free to experiment on other environments since the system runs in **Docker containers**.  

```bash

cd eds -> cd EDS
Update environment variables as needed:
nano .env

After proper configuration, start the containers one by one.

🚀 Components Setup

🔸 Elasticsearch

docker-compose up -d elasticsearch
docker logs -f eds-elasticsearch-1

Generate a service token:

curl -X POST --user elastic:changeme 0.0.0.0:9200/_security/service/elastic/kibana/credential/token/token1?pretty

Add the generated key into the kibana section of your docker-compose.yml:

nano docker-compose.yml

🔸 Kibana

docker-compose up -d kibana
docker logs -f eds-kibana-1

🔸 Filebeat

docker-compose build --no-cache filebeat
docker-compose up -d filebeat
docker logs -f eds-filebeat-1

🔸 Zeek

docker-compose build --no-cache zeek
docker-compose up -d zeek
docker logs -f eds-zeek-1

🔸 Suricata

docker-compose build --no-cache suricata
docker-compose up -d suricata
docker logs -f eds-suricata-1
Note: Custom rules have been added in the suricata folder for detecting DoS attacks, SQL injections, and privilege escalation attempts.
You can also create your own rules for detecting custom attacks.

🔸 Slips

docker-compose build --no-cache slips
docker-compose up -d slips
docker logs -f eds-slips-1

📊 Visualization

Logs and alerts are aggregated into Elasticsearch

Visualized in Kibana dashboards

Provides a unified view of threat activity across multiple IDS sources

🖼️ Architecture Diagram

<img width="1300" height="721" alt="image" src="https://github.com/user-attachments/assets/87e7b54f-936c-430f-bf56-9f9259e8c0a6" />


✅ Conclusion
The Ensemble Defense System (EDS) demonstrates the potential of hybrid IDS frameworks in modern security operations.
By combining signature-based, behavior-based, and SIEM-driven correlation, defenders can achieve:

📌 Better visibility into network activity

📌 Stronger detection of advanced threats

📌 More reliable alerts with fewer false positives

