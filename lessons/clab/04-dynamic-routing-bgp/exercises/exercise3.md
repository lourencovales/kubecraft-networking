1.

```bash
$ 04-dynamic-routing-bgp sudo docker exec -it clab-dynamic-routing-bgp-srl3 sr_cli -c "show network-instance default protocols bgp neighbor 10.1.3.1 detail"
----------------------------------------------------------------------------------------------------------------------
Peer : 10.1.3.1, remote AS: 65001, local AS: 65003, peer-type : ebgp
Type : static
Description : None
Group : ebgp-peers
Export policies : []
Import policies: ['import-all']
Under maintenance: False
Maintenance group:
----------------------------------------------------------------------------------------------------------------------
Admin-state is enable, session-state is established, up for 0d:1h:14m:28s
TCP connection is 10.1.3.2 [46493] -> 10.1.3.1 [179]
TCP-MD5 authentication is disabled
0 messages in input queue, 0 messages in output queue
----------------------------------------------------------------------------------------------------------------------
Last-state was openconfirm, last-event was recvOpen, 1 peer-flaps
Last received Notification was Error: None SubError: None
Failure detection: BFD is False, fast-failover is True
----------------------------------------------------------------------------------------------------------------------
Graceful Restart
   Admin State : disable
   Restarts by the peer : None
   Last restart : N/A
   Peer requested restart-time : None
   Stale routes time : None
----------------------------------------------------------------------------------------------------------------------
              Timer                      Configured          Operational                      Next
=================================================================================================================
connect-retry                               120                  120                           -
keepalive-interval                           30                   30                           -
hold-time                                    90                   90                           -
minimum-advertisement-interval               5                    5                            -
prefix-limit-restart-timer                   0                    0                            -
----------------------------------------------------------------------------------------------------------------------
Cap Sent:  ROUTE_REFRESH 4-OCTET_ASN MP_BGP GRACEFUL_RESTART
Cap Recv:  ROUTE_REFRESH 4-OCTET_ASN MP_BGP GRACEFUL_RESTART
----------------------------------------------------------------------------------------------------------------------
           Messages                            Sent                             Received                  Last
================================================================================================================
Non Updates                                     151                                151
Updates                                          5                                  4                   2026-04-
                                                                                                        01T12:26
                                                                                                        :15.000Z
Malformed updates                                0                                  0
Route Refreshes                                  0                                  0
----------------------------------------------------------------------------------------------------------------------
Ipv4-unicast AFI/SAFI
    End of RIB                     : sent, received
    Received routes                : 5
    Rejected routes                : None
    Active routes                  : 2
    Advertised routes              : None
    Prefix-limit-received          : 4294967295 routes, warning at 90, prevent-teardown False
    Prefix-limit-accepted          : None
    Default originate              : disabled
    Advertise with IPv6 next-hops  : False
    Peer requested GR helper       : None
    Peer preserved forwarding state: None
----------------------------------------------------------------------------------------------------------------------
```

```bash
$ 04-dynamic-routing-bgp sudo docker exec clab-dynamic-routing-bgp-host1 ping -c 3 10.1.5.2
PING 10.1.5.2 (10.1.5.2) 56(84) bytes of data.
From 10.1.1.1 icmp_seq=1 Destination Net Unreachable
From 10.1.1.1 icmp_seq=2 Destination Net Unreachable
From 10.1.1.1 icmp_seq=3 Destination Net Unreachable

--- 10.1.5.2 ping statistics ---
3 packets transmitted, 0 received, +3 errors, 100% packet loss, time 2040ms

$ 04-dynamic-routing-bgp sudo docker exec -it clab-dynamic-routing-bgp-srl3 sr_cli
Using configuration file(s): []
Welcome to the srlinux CLI.
Type 'help' (and press <ENTER>) if you need any help using this.
--{ + running }--[  ]--
A:srl3# enter candidate
--{ + candidate shared default }--[  ]--
A:srl3# set / network-instance default protocols bgp group ebgp-peers export-policy [export-connected export-bgp]
--{ +* candidate shared default }--[  ]--
A:srl3# commit now
All changes have been committed. Leaving candidate mode.
--{ + running }--[  ]--
A:srl3# exit
--{ + running }--[  ]--
A:srl3#
EOF encountered
$ 04-dynamic-routing-bgp sudo docker exec clab-dynamic-routing-bgp-host1 ping -c 3 10.1.5.2
PING 10.1.5.2 (10.1.5.2) 56(84) bytes of data.
64 bytes from 10.1.5.2: icmp_seq=1 ttl=62 time=0.321 ms
64 bytes from 10.1.5.2: icmp_seq=2 ttl=62 time=0.217 ms
64 bytes from 10.1.5.2: icmp_seq=3 ttl=62 time=0.202 ms

--- 10.1.5.2 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2033ms
rtt min/avg/max/mdev = 0.202/0.246/0.321/0.052 ms
```
