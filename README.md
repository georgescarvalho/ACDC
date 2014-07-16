# Global Fields Harmonization

Field|Format|Defined Values|Level Req.|Example|Field Description|
|---|---|---|---|---|-----------|
|timestamp|datetime(ISO8601)|-dynamic-|MUST|2014-07-15T00:16:29+00:00||
|source_key|string|["ip"/ "domain"/ "url"/ "email"/ "uri" / "sample"]|MUST|domain|....|
|source_value|string|-dynamic-|MUST|-dynamic-|...|
|type|string|[check sensors type values](http://nowhere.com)|MUST|malicious-website|....|
|confidence|string|[check sensors confidence values](http://nowhere.com)|MUST|TBD|....|
|description|string|-dynamic-|MUST|-dynamic-|Free text characterising the report and should be used for human readable|


## DDoS Fields Harmonization
Field|Format|Defined Values|Level Req.|Example|Field Description|
|---|---|---|---|---|-----------|
|source_key|string|"ip"|MUST|"ip"|-|
|source_value|[ipv4/ipv6]|-dynamic-|MUST|193.136.2.192|-|
|source_port|int|-dynamic|SHOULD|4234|-|
|destination_key|string|"ip"|MUST|"ip"|-|
|destination_value|[ipv4/ipv6]|-dynamic-|SHOULD|34.34.2.192|-|
|destination_port|int|-dynamic-|SHOULD|53|-|
|transport_protocol|string|[TCP/UDP/ICMP]|MUST|udp|Thissfield is used to give ifnroamtion about the attack for example attack by UDP Flooding...|
|asn|int|-dynamic-|SHOULD|1930|Autonous System Number|


### Case: Bot

This case present a case where an IP is a MUST and how all dataset behaves based on that.

**Dataset**

Field|Defined Values|Level Req.|
|---|---|---|
|source_time|(dynamic)|MUST|
|key|ip|MUST|
|type|"ddos-bot"|MUST|
|source_ip|-dynamic-|MUST|
|destination_ip|-dynamic-|MUST|
|transport_protocol|-dynamic-|MUST|
|description|-dynamic|MUST|
|confidence|MEDIUM|MUST|

**JSON Example**
```
{
 "source_time": "2014-07-15T00:16:29+00:00",
 "key": "ip",
 "type": "ddos-bot",
 "confidence": "medium",
 "description": "This is an event related to DoS attack...",
 "source_ip": "192.13.6.215",
 "destination_ip": "193.132.123.2",
 "transport_protocol": "udp"
}
```


# Data Semantic Analysis

### Network Semantics

```
ddos victim <- ddos attacker
source_ip = attacker
destin_ip = victim  
```

**Problem:**
* in a case where the job sensor is detect C&C or Vulnerable systems, in which key (source_ip/destination_ip) should sensor filled?

### Event Type Semantics

```
tipo = "ddos-victim"
ddos victim <- ddos attacker
source_ip = victim
destin_ip = atacker  
```

**Problem:**
* visualization, search for malicious activity, etc.., it will be more difficult to select all IPs related to victim systems and all IPs related to attackers systems.

**Example (select all attackers):**
```
search index=ACDC | list events (if type="ddos-bot": select source_ip ; if type="malicious-url": select ...)
```



# DEPRECATED

### [DEPRECATED] Dataset: C&C (DOMAIN MUST)

|Title|Field|Defined Values|Level Req.|
|:---:|:---:|:---:|:---:|
|Event Timestamp|source_time|(dynamic)|MUST|
|Key|key|"domain"|MUST|
|Type|type|"ddos-c&c"|MUST|
|Source Domain|source_domain|(dynamic)|MUST|
|Description|description|-dynamic|MUST|
