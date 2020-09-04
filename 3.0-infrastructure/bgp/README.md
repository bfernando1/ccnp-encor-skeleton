# Exam Topics 


## 3.2.c Configure and verify eBGP between directly connected neighbors (best path selection algorithm and neighbor relationships)

Private ASN

> * 64,512-65,535
> * 4,200,000,000-4,294,967,294


Path Attributes 

> provides BGP with granularity and control of routing policies within BGP
> * Well-known mandatory (required)
> * Well-known discretionary
> * Optional transitive
> * Optional non-transitive 


AS_PATH

> * used for loop prevention 
> * contains a complete list of all the ASNs that the prefix advertisement has
>   traversed from its source AS 


Multiprotocol BGP (MBGP) 

> * used to include ipv6 
> * AFI: Address Family Indicator (IPv4, IPv6) 
> * sAFI: subsequent AFI (unicast, multicast) 


## Configure eBGP 

```
R0#sh run | section bgp
router bgp 100
 bgp log-neighbor-changes
 no synchronization
 neighbor 10.1.1.6 remote-as 200
 network 10.1.1.4 mask 255.255.255.252
 network 1.1.1.1 mask 255.255.255.255
```

 
## Verify eBGP neighbors 

```
sh ip bgp 
sh ip bgp neighbors 
sh ip bgp summary 
sh ip route 
```


## BGP Messages 

Type | Name | Description 
--- | --- | ---
1 | OPEN | Sets up and establish BGP adjacency 
2 | UPDATE | Advertises, updates, or withdraws routes
3 | NOTIFICATION | Indicates an error condition to a BGP neighbor 
4 | KEEPALIVE | Ensures that neighbors are still alive 


OPEN messages

> session capabilites negotiated
> * BGP version number 
> * ASN of the originating router
> * hold time (cisco default = 180s) 
> * BGP ID (RID)


KEEPALIVE Messages 

> * 1/3 of OPEN message 


UPDATE Messages 

> * advertises any feasible routes 


NOTIFICATION Messages

> sends messages when error is detected 
> * hold timer expiring 
> * neighbor capabilites changing 
> * BGP session rest requested 


## BGP Neighbor States 

> * Idle
> * Connect
> * Active
> * OpenSent
> * OpenConfirm
> * Established

OpenSent Negotiations 

> * BGP versions must match.
> * The source IP address of the OPEN message must match the IP address that is  
> configured for the neighbor.
> * The AS number in the OPEN message must match what is configured for the neighbor.
> * BGP identifiers (RIDs) must be unique. If a RID does not exist, this
> condition is not met.
> * Security parameters (such as password and tine-to-live [TTL]) must be set
>  appropriately.


## BGP Path Selection 

> We love oranges as oranges mean pure refreshment 
> * Prefer the highest weight
> * Prefer the highest local preference
> * Prefer the route originated by the local router
> * Prefer the path with the shorter Accumulated Interior Gateway Protocol (AIGP) metric attribute
> * Prefer the shortest AS_Path
> * Prefer the best origin code
> * Prefer the lowest multi-exit discriminator (MED)
> * Prefer an external path over an internal path
> * Prefer the path through the closest IGP neighbor
> * Prefer the oldest route for eBGP paths
> * Prefer the path with the lowest neighbor BGP RID
> * Prefer the path with the lowest neighbor IP address
