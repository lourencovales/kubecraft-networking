Pings that worked:
from clab-ip-fundamentals-host1 to 10.1.1.1
from clab-ip-fundamentals-host2 to 10.1.3.1
from clab-ip-fundamentals-srl1 to 10.1.2.2

Pings that failed:
from clab-ip-fundamentals-host1 to 10.1.3.2

ARP tables:
$ 02-ip-fundamentals sudo docker exec clab-ip-fundamentals-host1 arp -n
? (10.1.1.1) at 1a:45:02:ff:00:01 [ether]  on eth1
? (172.20.20.1) at 9a:c8:c7:e8:36:10 [ether]  on eth0

$ 02-ip-fundamentals sudo docker exec -it clab-ip-fundamentals-srl1 sr_cli -c "show arpnd arp-entries"
+-----------+-----------+----------------+-----------+--------------------+----------------------------------------+
| Interface | Subinterf |    Neighbor    |  Origin   | Link layer address |                 Expiry                 |
|           |    ace    |                |           |                    |                                        |
+===========+===========+================+===========+====================+========================================+
| ethernet- |         0 |       10.1.1.2 |   dynamic | AA:C1:AB:43:89:39  | 3 hours from now                       |
| 1/1       |           |                |           |                    |                                        |
| ethernet- |         0 |       10.1.2.2 |   dynamic | 1A:E6:03:FF:00:01  | 3 hours from now                       |
| 1/2       |           |                |           |                    |                                        |
| mgmt0     |         0 |    172.20.20.1 |   dynamic | 9A:C8:C7:E8:36:10  | 3 hours from now                       |
+-----------+-----------+----------------+-----------+--------------------+----------------------------------------+
----------------------------------------------------------------------------------------------------------------------
  Total entries : 3 (0 static, 3 dynamic)
----------------------------------------------------------------------------------------------------------------------

The pings that failed (cross-subnet ones) did so because there are no routes to host that path - only host2 has a link to srl2; host1 is only connected to srl1
