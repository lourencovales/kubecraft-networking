1. It's missing the routes for 10.1.5.0/24
2. host2 <-> host3 requires the route on srl2 since all traffic must pass through there, and srl2 doesn't know how to forward it
3. The summary from the route-table on srl2 was clear enough on what was missing - this is the trouble with hub-and-spoke + static configs
