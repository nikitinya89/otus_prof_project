# otus_prof_project


| Server                      | In Interface  | Protocol | Port   | Source          | Destination     | Action  | State               | Description                |
|-----------------------------|---------------|----------|--------|-----------------|-----------------|---------|---------------------|----------------------------|
|**Frontend**                 | lo            | All      | Any    | 0.0.0.0/0       | 0.0.0.0/0       | Accept  |                     | Accept traffic to loopback |
|                             | any           | All      | Any    | 0.0.0.0/0       | 0.0.0.0/0       | Accept  | Established Related | Accepted established       |
|                             | any           | All      | Any    | 0.0.0.0/0       | 0.0.0.0/0       | Drop    | Invalid             | Drop invalid               |
|                             | enp0s8        | TCP      | 22     | 0.0.0.0/0       | 0.0.0.0/0       | Accept  | New                 | SSH                        |
|                             | enp0s9        | TCP      | 80, 443| 0.0.0.0/0       | 0.0.0.0/0       | Accept  | New                 | HTTP / HTTPS               |
|                             | enp0s8        | TCP      | 80, 443| 0.0.0.0/0       | 0.0.0.0/0       | Accept  | New                 | HTTP / HTTPS               |
|                             | enp0s8        | TCP      | 9100   | 192.168.56.106  | 0.0.0.0/0       | Accept  | New                 | Node exporter              |
|                             | enp0s8        | TCP      | 9100   | 192.168.56.106  | 0.0.0.0/0       | Accept  | New                 | Nginx exporter             |
|                             | any           | ICMP     | Any    | 0.0.0.0/0       | 0.0.0.0/0       | Accept  |                     |                            |
|                             |               |          |        |                 |                 |         |                     |                            |
|**Backend-1** / **Backend-2**| lo            | All      | Any    | 0.0.0.0/0       | 0.0.0.0/0       | Accept  |                     | Accept traffic to loopback |
|                             | any           | All      | Any    | 0.0.0.0/0       | 0.0.0.0/0       | Accept  | Established Related | Accepted established       |
|                             | any           | All      | Any    | 0.0.0.0/0       | 0.0.0.0/0       | Drop    | Invalid             | Drop invalid               |



|**DB-Master** / **DB-Slave**| lo            | All      | Any    | 0.0.0.0/0       | 0.0.0.0/0       | Accept  |                     | Accept traffic to loopback |

