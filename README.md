# otus_prof_project

![Network map](img/network.jpg)

| Server Name    | Private IP-address | Public IP-address | Description                  |
|----------------|--------------------|-------------------|------------------------------|
| **Frontend**   | 192.168.56.101     | 192.168.1.101     | Frontend web server          |
| **Backend-1**  | 192.168.56.102     | -                 | Backend web server           |
| **Backend-2**  | 192.168.56.103     | -                 | Backend web server           |
| **DB_Master**  | 192.168.56.104     | -                 | MySQL Server Master          |
| **DB_Slave**   | 192.168.56.105     | -                 | MySQL Server Replica         |
| **Monitoring** | 192.168.56.106     | -                 | Monitoring server. GAP Stack |
| **Log**        | 192.168.56.107     | -                 | Log Server. ELK Stack        |
  

  
| Server                        | In Interface  | Protocol | Port       | Source          | Destination     | Action  | State               | Description                |
|-------------------------------|---------------|----------|------------|-----------------|-----------------|---------|---------------------|----------------------------|
| **Frontend**                  | lo            | All      | Any        | 0.0.0.0/0       | 0.0.0.0/0       | Accept  |                     | Accept traffic to loopback |
|                               | any           | All      | Any        | 0.0.0.0/0       | 0.0.0.0/0       | Accept  | Established Related | Accepted established       |
|                               | any           | All      | Any        | 0.0.0.0/0       | 0.0.0.0/0       | Drop    | Invalid             | Drop invalid               |
|                               | enp0s8        | TCP      | 22         | 0.0.0.0/0       | 0.0.0.0/0       | Accept  | New                 | SSH                        |
|                               | enp0s9        | TCP      | 80, 443    | 0.0.0.0/0       | 0.0.0.0/0       | Accept  |                     | HTTP / HTTPS               |
|                               | enp0s8        | TCP      | 80, 443    | 0.0.0.0/0       | 0.0.0.0/0       | Accept  |                     | HTTP / HTTPS               |
|                               | enp0s8        | TCP      | 9100       | 192.168.56.106  | 0.0.0.0/0       | Accept  |                     | Node exporter              |
|                               | enp0s8        | TCP      | 9113       | 192.168.56.106  | 0.0.0.0/0       | Accept  |                     | Nginx exporter             |
|                               | any           | ICMP     | Any        | 0.0.0.0/0       | 0.0.0.0/0       | Accept  |                     | Accept ICMP                |
|                               |               |          |            |                 |                 |         |                     |                            |
| **Backend-1** / **Backend-2** | lo            | All      | Any        | 0.0.0.0/0       | 0.0.0.0/0       | Accept  |                     | Accept traffic to loopback |
|                               | any           | All      | Any        | 0.0.0.0/0       | 0.0.0.0/0       | Accept  | Established Related | Accepted established       |
|                               | any           | All      | Any        | 0.0.0.0/0       | 0.0.0.0/0       | Drop    | Invalid             | Drop invalid               |
|                               | enp0s8        | TCP      | 22         | 0.0.0.0/0       | 0.0.0.0/0       | Accept  | New                 | SSH                        |
|                               | enp0s8        | TCP      | 80, 443    | 0.0.0.0/0       | 0.0.0.0/0       | Accept  |                     | HTTP / HTTPS               |
|                               | enp0s8        | TCP      | 9100       | 192.168.56.106  | 0.0.0.0/0       | Accept  |                     | Node exporter              |
|                               | any           | ICMP     | Any        | 0.0.0.0/0       | 0.0.0.0/0       | Accept  |                     | Accept ICMP                |
|                               |               |          |            |                 |                 |         |                     |                            |
| **DB-Master**                 | lo            | All      | Any        | 0.0.0.0/0       | 0.0.0.0/0       | Accept  |                     | Accept traffic to loopback |
|                               | any           | All      | Any        | 0.0.0.0/0       | 0.0.0.0/0       | Accept  | Established Related | Accepted established       |
|                               | any           | All      | Any        | 0.0.0.0/0       | 0.0.0.0/0       | Drop    | Invalid             | Drop invalid               |
|                               | enp0s8        | TCP      | 22         | 0.0.0.0/0       | 0.0.0.0/0       | Accept  | New                 | SSH                        |
|                               | enp0s8        | TCP      | 3306       | 192.168.56.102  | 0.0.0.0/0       | Accept  |                     | MySQL for Backend-1        |
|                               | enp0s8        | TCP      | 3306       | 192.168.56.103  | 0.0.0.0/0       | Accept  |                     | MySQL for Backend-2        |
|                               | enp0s8        | TCP      | 3306       | 192.168.56.105  | 0.0.0.0/0       | Accept  |                     | MySQL for DB-Slave         |
|                               | enp0s8        | TCP      | 9100       | 192.168.56.106  | 0.0.0.0/0       | Accept  |                     | Node exporter              |
|                               | enp0s8        | TCP      | 9104       | 192.168.56.106  | 0.0.0.0/0       | Accept  |                     | MySQL exporter             |
|                               | any           | ICMP     | Any        | 0.0.0.0/0       | 0.0.0.0/0       | Accept  |                     | Accept ICMP                |
|                               |               |          |            |                 |                 |         |                     |                            |
| **DB-Slave**                  | lo            | All      | Any        | 0.0.0.0/0       | 0.0.0.0/0       | Accept  |                     | Accept traffic to loopback |
|                               | any           | All      | Any        | 0.0.0.0/0       | 0.0.0.0/0       | Accept  | Established Related | Accepted established       |
|                               | any           | All      | Any        | 0.0.0.0/0       | 0.0.0.0/0       | Drop    | Invalid             | Drop invalid               |
|                               | enp0s8        | TCP      | 22         | 0.0.0.0/0       | 0.0.0.0/0       | Accept  | New                 | SSH                        |
|                               | enp0s8        | TCP      | 3306       | 192.168.56.102  | 0.0.0.0/0       | Accept  |                     | MySQL for Backend-1        |
|                               | enp0s8        | TCP      | 3306       | 192.168.56.103  | 0.0.0.0/0       | Accept  |                     | MySQL for Backend-2        |
|                               | enp0s8        | TCP      | 3306       | 192.168.56.104  | 0.0.0.0/0       | Accept  |                     | MySQL for DB-Master        |
|                               | enp0s8        | TCP      | 9100       | 192.168.56.106  | 0.0.0.0/0       | Accept  |                     | Node exporter              |
|                               | enp0s8        | TCP      | 9104       | 192.168.56.106  | 0.0.0.0/0       | Accept  |                     | MySQL exporter             |
|                               | any           | ICMP     | Any        | 0.0.0.0/0       | 0.0.0.0/0       | Accept  |                     | Accept ICMP                |
|                               |               |          |            |                 |                 |         |                     |                            |
| **Monitoring**                | lo            | All      | Any        | 0.0.0.0/0       | 0.0.0.0/0       | Accept  |                     | Accept traffic to loopback |
|                               | any           | All      | Any        | 0.0.0.0/0       | 0.0.0.0/0       | Accept  | Established Related | Accepted established       |
|                               | any           | All      | Any        | 0.0.0.0/0       | 0.0.0.0/0       | Drop    | Invalid             | Drop invalid               |
|                               | enp0s8        | TCP      | 22         | 0.0.0.0/0       | 0.0.0.0/0       | Accept  | New                 | SSH                        |
|                               | enp0s8        | TCP      | 9090       | 0.0.0.0/0       | 0.0.0.0/0       | Accept  |                     | Prometheus                 |
|                               | enp0s8        | TCP      | 3000       | 0.0.0.0/0       | 0.0.0.0/0       | Accept  |                     | Grafana Server             |
|                               | enp0s8        | TCP      | 9093, 9094 | 0.0.0.0/0       | 0.0.0.0/0       | Accept  |                     | Alertmanager               |
|                               | enp0s8        | TCP      | 9100       | 192.168.56.106  | 0.0.0.0/0       | Accept  |                     | Node exporter              |
|                               | any           | ICMP     | Any        | 0.0.0.0/0       | 0.0.0.0/0       | Accept  |                     | Accept ICMP                |
|                               |               |          |            |                 |                 |         |                     |                            |
| **Log**                       | lo            | All      | Any        | 0.0.0.0/0       | 0.0.0.0/0       | Accept  |                     | Accept traffic to loopback |
|                               | any           | All      | Any        | 0.0.0.0/0       | 0.0.0.0/0       | Accept  | Established Related | Accepted established       |
|                               | an_           | All      | Any        | 0.0.0.0/0       | 0.0.0.0/0       | Drop    | Invalid             | Drop invalid               |
|                               | enp0s8        | TCP      | 22         | 0.0.0.0/0       | 0.0.0.0/0       | Accept  | New                 | SSH                        |
|                               | enp0s8        | TCP      | 9200       | 0.0.0.0/0       | 0.0.0.0/0       | Accept  |                     | Elasticsearch              |
|                               | enp0s8        | TCP      | 5601       | 0.0.0.0/0       | 0.0.0.0/0       | Accept  |                     | Kibana                     |
|                               | enp0s8        | TCP      | 5044       | 0.0.0.0/0       | 0.0.0.0/0       | Accept  |                     | Logstash                   |
|                               | enp0s8        | TCP      | 9100       | 192.168.56.106  | 0.0.0.0/0       | Accept  |                     | Node exporter              |
|                               | any           | ICMP     | Any        | 0.0.0.0/0       | 0.0.0.0/0       | Accept  |                     | Accept ICMP                |

























