# Lab : Understand how EIGRP in depth

## Objective
Really understand how the EIGRP metric is evaluated to choose the best path. And confirm it uses the sum of the delay on the path to the destination route and the minimum bandwidth

## Technology in use
- Router
- Cisco Packet Tracer
- EIGRP Protocol


## Topologie
see the image in the topology file in the repo

## Step
1. Make the topologie
We choose 5 routers some of them can be in the same super domain to explore the auto-summary functionality of the EIGRP protocol some of the router can reach the same end destination to explore the unequal-CMP capability of the protocol. one of them especially one close to the end device connected has a FastEthernet links to explore how the metric is calculated very well. In our case router 4 (It can be router 5 too)

2. Configure ip address of the devices according to the addresse's topology. 


3. Configure EIGRP set the side through the end device as a passive-interface to not waste bandwidth

4. check all the the bandwidth of each interfaces FastEthernet (100000 kbit, delay 100) and GigabitEthernet(1000000 kbit, delay 10). We will be able to see how the routing protocol use slowest bandwidth and all delay. That's what will be advertise by every router to his other connected router to calculate the metric (composite metric).

5. set EIGRP on all routers with an AS of 1

6. When we check the routing table on router R1 we see 3584 as the metric and the delay is 40. We can see the path is the one via router R5 because each delays in every routers to R1 is 10 if the interface is a GigabitEthernet type. let's check the calculation, typically in a network where only bandwidth and delay are considered, the formula of the metric is: 
$metric = 256 * ( bandwidth + delay )$
the metric is scaled by 10^7 divided by the minimum bandwidth in kilobit per second and the delay is scaled by dividing by 10
the calculation then is $Metric = 256 * ((10^7/10^6) + 4)$
and the answer equal 3584 the same metric we saw when we check R1 routing table

- first conclusion EIGRP really use sum of delays
- next, The general formula to calculate the metric in EIGRP route function quite well.

7. Add loopback addresses on some routers to explore the router-id default selection of the protocol (i will add on router 1 and 3)

## include files
routers configuration
network topology
router R1 route to the test destination file
[packet tracer file] at the end of the lab test



## What i have learned
Really understand how the metric is evaluated in the EIGRP protocol.

