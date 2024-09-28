# otus_prof_project

| Server Name    | Private IP-address | Public IP-address | Description                  |
|----------------|--------------------|-------------------|------------------------------|
| **Frontend**   | 192.168.56.101     | 192.168.1.101     | Frontend web server          |
| **Backend-1**  | 192.168.56.102     | -                 | Backend web server           |
| **Backend-2**  | 192.168.56.103     | -                 | Backend web server           |
| **DB_Master**  | 192.168.56.104     | -                 | MySQL Server Master          |
| **DB_Slave**   | 192.168.56.105     | -                 | MySQL Server Replica         |
| **Monitoring** | 192.168.56.106     | -                 | Monitoring server. GAP Stack |
| **Log**        | 192.168.56.107     | -                 | Log Server. ELK Stack        |
  

  
| Server                        | In Interface    | Protocol | Port       | Source          | Destination     | Action  | State               | Description                |
|-------------------------------|-----------------|----------|------------|-----------------|-----------------|---------|---------------------|----------------------------|
| **Frontend**                  | _lo_            | All      | Any        | 0.0.0.0/0       | 0.0.0.0/0       | Accept  |                     | Accept traffic to loopback |
|                               | _any_           | All      | Any        | 0.0.0.0/0       | 0.0.0.0/0       | Accept  | Established Related | Accepted established       |
|                               | _any_           | All      | Any        | 0.0.0.0/0       | 0.0.0.0/0       | Drop    | Invalid             | Drop invalid               |
|                               | _enp0s8_        | TCP      | 22         | 0.0.0.0/0       | 0.0.0.0/0       | Accept  | New                 | SSH                        |
|                               | _enp0s9_        | TCP      | 80, 443    | 0.0.0.0/0       | 0.0.0.0/0       | Accept  |                     | HTTP / HTTPS               |
|                               | _enp0s8_        | TCP      | 80, 443    | 0.0.0.0/0       | 0.0.0.0/0       | Accept  |                     | HTTP / HTTPS               |
|                               | _enp0s8_        | TCP      | 9100       | 192.168.56.106  | 0.0.0.0/0       | Accept  |                     | Node exporter              |
|                               | _enp0s8_        | TCP      | 9113       | 192.168.56.106  | 0.0.0.0/0       | Accept  |                     | Nginx exporter             |
|                               | _any_           | ICMP     | Any        | 0.0.0.0/0       | 0.0.0.0/0       | Accept  |                     | Accept ICMP                |
|                               |                 |          |            |                 |                 |         |                     |                            |
| **Backend-1** / **Backend-2** | _lo_            | All      | Any        | 0.0.0.0/0       | 0.0.0.0/0       | Accept  |                     | Accept traffic to loopback |
|                               | _any_           | All      | Any        | 0.0.0.0/0       | 0.0.0.0/0       | Accept  | Established Related | Accepted established       |
|                               | _any_           | All      | Any        | 0.0.0.0/0       | 0.0.0.0/0       | Drop    | Invalid             | Drop invalid               |
|                               | _enp0s8_        | TCP      | 22         | 0.0.0.0/0       | 0.0.0.0/0       | Accept  | New                 | SSH                        |
|                               | _enp0s8_        | TCP      | 80, 443    | 0.0.0.0/0       | 0.0.0.0/0       | Accept  |                     | HTTP / HTTPS               |
|                               | _enp0s8_        | TCP      | 9100       | 192.168.56.106  | 0.0.0.0/0       | Accept  |                     | Node exporter              |
|                               | _any_           | ICMP     | Any        | 0.0.0.0/0       | 0.0.0.0/0       | Accept  |                     | Accept ICMP                |
|                               |                 |          |            |                 |                 |         |                     |                            |
| **DB-Master**                 | _lo_            | All      | Any        | 0.0.0.0/0       | 0.0.0.0/0       | Accept  |                     | Accept traffic to loopback |
|                               | _any_           | All      | Any        | 0.0.0.0/0       | 0.0.0.0/0       | Accept  | Established Related | Accepted established       |
|                               | _any_           | All      | Any        | 0.0.0.0/0       | 0.0.0.0/0       | Drop    | Invalid             | Drop invalid               |
|                               | _enp0s8_        | TCP      | 22         | 0.0.0.0/0       | 0.0.0.0/0       | Accept  | New                 | SSH                        |
|                               | _enp0s8_        | TCP      | 3306       | 192.168.56.102  | 0.0.0.0/0       | Accept  |                     | MySQL for Backend-1        |
|                               | _enp0s8_        | TCP      | 3306       | 192.168.56.103  | 0.0.0.0/0       | Accept  |                     | MySQL for Backend-2        |
|                               | _enp0s8_        | TCP      | 3306       | 192.168.56.105  | 0.0.0.0/0       | Accept  |                     | MySQL for DB-Slave         |
|                               | _enp0s8_        | TCP      | 9100       | 192.168.56.106  | 0.0.0.0/0       | Accept  |                     | Node exporter              |
|                               | _enp0s8_        | TCP      | 9104       | 192.168.56.106  | 0.0.0.0/0       | Accept  |                     | MySQL exporter             |
|                               | _any_           | ICMP     | Any        | 0.0.0.0/0       | 0.0.0.0/0       | Accept  |                     | Accept ICMP                |
|                               |                 |          |            |                 |                 |         |                     |                            |
| **DB-Slave**                  | _lo_            | All      | Any        | 0.0.0.0/0       | 0.0.0.0/0       | Accept  |                     | Accept traffic to loopback |
|                               | _any_           | All      | Any        | 0.0.0.0/0       | 0.0.0.0/0       | Accept  | Established Related | Accepted established       |
|                               | _any_           | All      | Any        | 0.0.0.0/0       | 0.0.0.0/0       | Drop    | Invalid             | Drop invalid               |
|                               | _enp0s8_        | TCP      | 22         | 0.0.0.0/0       | 0.0.0.0/0       | Accept  | New                 | SSH                        |
|                               | _enp0s8_        | TCP      | 3306       | 192.168.56.102  | 0.0.0.0/0       | Accept  |                     | MySQL for Backend-1        |
|                               | _enp0s8_        | TCP      | 3306       | 192.168.56.103  | 0.0.0.0/0       | Accept  |                     | MySQL for Backend-2        |
|                               | _enp0s8_        | TCP      | 3306       | 192.168.56.104  | 0.0.0.0/0       | Accept  |                     | MySQL for DB-Master        |
|                               | _enp0s8_        | TCP      | 9100       | 192.168.56.106  | 0.0.0.0/0       | Accept  |                     | Node exporter              |
|                               | _enp0s8_        | TCP      | 9104       | 192.168.56.106  | 0.0.0.0/0       | Accept  |                     | MySQL exporter             |
|                               | _any_           | ICMP     | Any        | 0.0.0.0/0       | 0.0.0.0/0       | Accept  |                     | Accept ICMP                |
|                               |                 |          |            |                 |                 |         |                     |                            |
| **Monitoring**                | _lo_            | All      | Any        | 0.0.0.0/0       | 0.0.0.0/0       | Accept  |                     | Accept traffic to loopback |
|                               | _any_           | All      | Any        | 0.0.0.0/0       | 0.0.0.0/0       | Accept  | Established Related | Accepted established       |
|                               | _any_           | All      | Any        | 0.0.0.0/0       | 0.0.0.0/0       | Drop    | Invalid             | Drop invalid               |
|                               | _enp0s8_        | TCP      | 22         | 0.0.0.0/0       | 0.0.0.0/0       | Accept  | New                 | SSH                        |
|                               | _enp0s8_        | TCP      | 9090       | 0.0.0.0/0       | 0.0.0.0/0       | Accept  |                     | Prometheus                 |
|                               | _enp0s8_        | TCP      | 3000       | 0.0.0.0/0       | 0.0.0.0/0       | Accept  |                     | Grafana Server             |
|                               | _enp0s8_        | TCP      | 9093, 9094 | 0.0.0.0/0       | 0.0.0.0/0       | Accept  |                     | Alertmanager               |
|                               | _enp0s8_        | TCP      | 9100       | 192.168.56.106  | 0.0.0.0/0       | Accept  |                     | Node exporter              |
|                               | _any_           | ICMP     | Any        | 0.0.0.0/0       | 0.0.0.0/0       | Accept  |                     | Accept ICMP                |
|                               |                 |          |            |                 |                 |         |                     |                            |
| **Log**                       | _lo_            | All      | Any        | 0.0.0.0/0       | 0.0.0.0/0       | Accept  |                     | Accept traffic to loopback |
|                               | _any_           | All      | Any        | 0.0.0.0/0       | 0.0.0.0/0       | Accept  | Established Related | Accepted established       |
|                               | _any_           | All      | Any        | 0.0.0.0/0       | 0.0.0.0/0       | Drop    | Invalid             | Drop invalid               |
|                               | _enp0s8_        | TCP      | 22         | 0.0.0.0/0       | 0.0.0.0/0       | Accept  | New                 | SSH                        |
|                               | _enp0s8_        | TCP      | 9200       | 0.0.0.0/0       | 0.0.0.0/0       | Accept  |                     | Elasticsearch              |
|                               | _enp0s8_        | TCP      | 5601       | 0.0.0.0/0       | 0.0.0.0/0       | Accept  |                     | Kibana                     |
|                               | _enp0s8_        | TCP      | 5044       | 0.0.0.0/0       | 0.0.0.0/0       | Accept  |                     | Logstash                   |
|                               | _enp0s8_        | TCP      | 9100       | 192.168.56.106  | 0.0.0.0/0       | Accept  |                     | Node exporter              |
|                               | _any_           | ICMP     | Any        | 0.0.0.0/0       | 0.0.0.0/0       | Accept  |                     | Accept ICMP                |



























