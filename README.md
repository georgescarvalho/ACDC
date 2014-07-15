# Global

|Title|Field|Format|Defined Values|Level Req.|Example|Description|
|---|---|---|---|---|---|-----------|
|Event Timestamp|source_time|datetime(ISO8601)|-|MUST|2014-07-15T00:16:29+00:00||
|Key|key|string|["ip"/"domain"/"url"/"email"/"uri"]|MUST|domain|....|
|Type|type|string|[check sensors type values](http://nowhere.com)|MUST|malicious-website|....|
|Confidence|confidence|string|[check sensors confidence values](http://nowhere.com)|MUST|TBD|....|
|Description|description|string|-|MUST|-|Free text characterising the report and should be used for human readable|

## DDoS Global
|Title|Field|Format|Defined Values|Level Req.|Example|Description|
|:---:|:---:|:---:|:---:|:---:|:---:|:-----------:|
|Source IP|source_ip|[ipv4/ipv6]|-|SHOULD|193.136.2.192|-|
|Source Port|source_port|int|-|SHOULD|4234|-|
|Destination IP|destination_ip|[ipv4/ipv6]|-|SHOULD|193.136.100.192|-|
|Destination Port|destination_port|int|-|SHOULD|53|-|
|Domain|domain|RFC123|-|SHOULD|www.botfree.eu|-|
|Transport Protocol|transport_protocol|string|[TCP/UDP/ICMP]|MUST|udp|This field is used to give ifnroamtion about the attack for example attack by UDP Flooding...|

### Case: Bot (IP Must)

**Dataset**

|Title|Field|Defined Values|Level Req.|
|:---:|:---:|:---:|:---:|
|Event Timestamp|source_time|(dynamic)|MUST|
|Key|key|ip|MUST|
|Type|type|"ddos-bot"|MUST|
|Source IP|source_ip|-dynamic-|MUST|
|Destination IP|destination_ip|-dynamic-|MUST|
|Transport Protocol|transport_protocol|-dynamic-|MUST|
|Description|description|-dynamic|MUST|
|Confidence|confidence|sensor is LOW|MUST|

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


### Dataset: C&C (DOMAIN MUST)
|Title|Field|Defined Values|Level Req.|
|:---:|:---:|:---:|:---:|
|Event Timestamp|source_time|(dynamic)|MUST|
|Key|key|"domain"|MUST|
|Type|type|"ddos-c&c"|MUST|
|Source Domain|source_domain|(dynamic)|MUST|
|Description|description|-dynamic|MUST|

### Cneas
|Source IP|source_ip|[ipv4/ipv6]|SHOULD|depends on network connection|
|Destination IP|destination_ip|[ipv4/ipv6]|MUST|depends on network connection|

Filosofia Network
===========
ddos victim <- ddos attacker
source_ip = attacker
destin_ip = victim  


Filosofia Tipo
===========
tipo = "ddos-victim"
ddos victim <- ddos attacker
source_ip = victim
destin_ip = atacker  
