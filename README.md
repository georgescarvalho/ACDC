# Global

Field|Format|Defined Values|Level Req.|Example|Field Description|
|---|---|---|---|---|-----------|
|timestamp|datetime(ISO8601)|-|MUST|2014-07-15T00:16:29+00:00||
|key|string|["ip"/ "domain"/ "url"/ "email"/ "uri"]|MUST|domain|....|
|type|string|[check sensors type values](http://nowhere.com)|MUST|malicious-website|....|
|confidence|string|[check sensors confidence values](http://nowhere.com)|MUST|TBD|....|
|description|string|-|MUST|-|Free text characterising the report and should be used for human readable|

**Note:** Should we remove 'key' field. Is seems redundant to have a key and then define the value for that key.
**Example:**
```
{
 "key": "ip",
 "source_ip": "192.13.6.215",
}
```
**Solution:**
```
{
 "source_ip": "192.13.6.215",
}
```

## DDoS Global
Field|Format|Defined Values|Level Req.|Example|Field Description|
|---|---|---|---|---|-----------|
|source_ip|[ipv4/ipv6]|-|SHOULD|193.136.2.192|-|
|source_port|int|-|SHOULD|4234|-|
|destination_ip|[ipv4/ipv6]|-|SHOULD|193.136.100.192|-|
|destination_port|int|-|SHOULD|53|-|
|domain|RFC123|-|SHOULD|www.botfree.eu|-|
|transport_protocol|string|[TCP/UDP/ICMP]|MUST|udp|This field is used to give ifnroamtion about the attack for example attack by UDP Flooding...|

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
|confidence|sensor is LOW|MUST|

**JSON Example**
```
{
 "source_time": "2014-07-15T00:16:29+00:00",
 "key": "ip",
 "type": "ddos-bot",
 "confidence": "low",
 "description": "This is an event related to DoS attack...",
 "source_ip": "192.13.6.215",
 "destination_ip": "193.132.123.2",
 "transport_protocol": "udp"
}
```


# Data Semantic Analysis

### Network Semantic

```
ddos victim <- ddos attacker
source_ip = attacker
destin_ip = victim  
```

### Event Type Semantics

```
tipo = "ddos-victim"
ddos victim <- ddos attacker
source_ip = victim
destin_ip = atacker  
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
