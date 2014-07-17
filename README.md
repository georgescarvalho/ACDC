# Global Fields Harmonization

|Field|Format|Defined Values|Level Req.|Example|Field Description|
|---|---|---|---|---|-----------|
|sensor|string|["thug", "glastopf", "dionaea", ...]|MUST|"thug"|Sensor Name|
|category|string|["ddos"]|(dynamic)|MUST|"ddos"|classification of the event...|
|subcategory|string|["flood"]|(dynamic)|MUST|"flood"|subclassification of the event...|
|description|string|(dynamic)|MUST|(dynamic)|Free text characterising the report and should be used for human readable|
|timestamp|datetime(ISO8601)|(dynamic)|MUST|2014-07-15T00:16:29+00:00|Event timestamp|
|source_key|string|["ip", "domain", "url", "email", "uri", "sample", "imei"]|MUST|domain|....|
|source_value|string|(dynamic)|MUST|(dynamic)|...|
|source_port|int|(dynamic)|MAY|246|-|
|source_asn|int|(dynamic)|MAY|1930|Autonous System Number|
|destination_key|string|["ip", "domain", "url", "email", "uri", "sample", "imei"]|MAY|domain|....|
|destination_value|string|(dynamic)|MAY|(dynamic)|...|
|destination_port|int|(dynamic)|MAY|53|-|
|destination_asn|int|(dynamic)|MAY|1232|Autonous System Number|
|transport_protocol|string|["tcp", "udp", "icmp"]|SHOULD|"udp"|This field is used to give infroamtion about the attack for example attack by UDP...|
|protocol|string|["dns", "http, "ssh"]|SHOULD|""|This field is used to give infroamtion about the attack for example attack though SSH|


**To Remove:**
```
|confidence|string|[check sensors confidence values](http://nowhere.com)|MUST|TBD|Level of confidence in source **(this value should not exist because CCH is who can decide in the central point)**|
```


## Bot Detection Reports Fields Harmonization

**Note:** Bot ip must be inserted in source_value and C&C ip must be inserted in destination_value.

Field|Format|Defined Values|Level Req.|Example|Field Description|
|---|---|---|---|---|-----------|
|source_key|string|"ip"|MUST|"ip"|-|
|source_value|[ipv4/ipv6]|(dynamic)|MUST|19.12.12.213|Bot ip|
|destination_key|string|"ip"|MUST|"ip"|-|
|destination_value|[ipv4/ipv6]|(dynamic)|MUST|34.34.2.192|C&C ip|
|type|string|"bot"|(dynamic)|MUST|"bot"|"Infected machine connected to C&C server."|


**Dataset**

Field|Defined Values|Level Req.|
|---|---|---|
|sensor|"thug"|MUST|
|category|"ddos"|MUST|
|subcategory|"flood"|MUST|
|timestamp|(dynamic)|MUST|
|confidence|MEDIUM|MUST|
|description|"DoS Attack from source to destination"|MUST|
|source_key|"ip"|MUST|
|source_value|(dynamic)|MUST|
|source_port|(dynamic)|MUST|
|source_asn|(dynamic)|SHOULD|
|destination_key|"ip"|MUST|
|destination_value|(dynamic)|MUST|
|destination_port|(dynamic)|MUST|
|destination_asn|(dynamic)|MAY|
|transport_protocol|(dynamic)|MUST|






## C&C Detection Reports Fields Harmonization

**Note:** C&C ip must be inserted in source_value.

Field|Format|Defined Values|Level Req.|Example|Field Description|
|---|---|---|---|---|-----------|
|source_key|string|"ip"|MUST|"ip"|-|
|source_value|[ipv4/ipv6]|(dynamic)|MUST|19.12.12.213|Bot ip|
|source_port|int|(dynamic)|SHOULD|246|-|
|transport_protocol|string|["tcp", "udp", "icmp"]|SHOULD|"udp"|This field is used to give infroamtion about the attack for example attack by UDP...|
|source_asn|int|(dynamic)|SHOULD|1967|Autonous System Number|



## DDoS Reports Fields Harmonization

Field|Format|Defined Values|Level Req.|Example|Field Description|
|---|---|---|---|---|-----------|
|source_key|string|"ip"|MUST|"ip"|-|
|source_value|[ipv4/ipv6]|(dynamic)|MUST|193.136.2.192|Attacker IP|
|source_port|int|-dynamic|SHOULD|4234|-|
|destination_key|string|"ip"|SHOULD|"ip"|-|
|destination_value|[ipv4/ipv6]|(dynamic)|SHOULD|34.34.2.192|Victim IP|
|destination_port|int|(dynamic)|SHOULD|53|-|
|transport_protocol|string|["TCP", "UDP", "ICMP"]|MUST|udp|This field is used to give ifnroamtion about the attack for example attack by UDP Flooding...|
|source_asn|int|(dynamic)|SHOULD|1930|Autonous System Number|



### Case: Report an Dos Attack.

**Note:** Source IP of attack must be inserted in source_value and 'destination IP' (victim) must be inserted in 'destination_value'.

**Dataset**

Field|Defined Values|Level Req.|
|---|---|---|
|sensor|"thug"|MUST|
|category|"ddos"|MUST|
|subcategory|"flood"|MUST|
|timestamp|(dynamic)|MUST|
|confidence|MEDIUM|MUST|
|description|"DoS Attack from source to destination"|MUST|
|source_key|"ip"|MUST|
|source_value|(dynamic)|MUST|
|source_port|(dynamic)|MUST|
|source_asn|(dynamic)|SHOULD|
|destination_key|"ip"|MUST|
|destination_value|(dynamic)|MUST|
|destination_port|(dynamic)|MUST|
|destination_asn|(dynamic)|MAY|
|transport_protocol|(dynamic)|MUST|


**JSON Example**

```
{
 "sensor": "thug",
 "category": "ddos",
 "subcategory": "flood",
 "timestamp": "2014-07-15T00:16:29+00:00",
 "confidence": "medium",
 "description": "DoS Attack from source to destination", 
 "source_key": "ip",
 "source_value": "192.135.6.215",
 "source_port": "53",
 "source_asn": "1930",
 "destination_key": "ip",
 "destination_value": "192.80.6.215", 
 "destination_port": "22",
 "destination_asn": "19165",
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


