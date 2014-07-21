# Dictionary

<a name="sensor-identification"></a>
### *Sensor Identification*
|Category|Sensor|Entity|
|---|---|---|
|ddos|DDoS Monitoring Tool|IF-IS|
|ddos| Black-Holing| DE-CIX |
|ddos|(...) | (...)|
||||
|website|initiative-S|ECO|
|website|Horga|ISCTI|
|website|Skanna|INTECO|
|website|Honeypot Sensor|CARNET|
|website| (...) | (...)|
||||
|fasstflux|Passive dns sensor| CARNET|
|fasstflux|DNS Traffic Sensor| ATOS|
|fasstflux|Flux Detect|INTECO|
|fasstflux| (...) | (...)|
||||
|mobile|Suricata IDS|XLAB|
|mobile|Conan mobile|INTECO|
|mobile| (...) | (...)|
||||
|spam|Spamtrap|CARNET|
|spam|Spambot detector|TID|
|spam|Spam analysis tool|CERT-RO|
|spam|AHPS|ATOS|
|spam| (...) | (...)|

<a name="events-classification"></a>
### *Events Classification*

|Category|SubCategory|
|---|---|
|ddos|flood|
|||
|website|malware|
|website|malicious content|
|website|vulnerable|
|||
stflux|malicious content|
|||
|mobile|malware|
|mobile|malicious content|
|mobile|**event**|
|||
|spam|malware|
|spam|malicious content|
|spam|campaign|



### *Field list*
**Description:**(tentar descrever a tabela)

|Field|Format|Defined Values|Field Description|
|---|---|---|-----------|
|sensor|string|[sensor list](#sensor-identification)|sensor name...|
|category|string|[categories list](#events-classification)|classification of the event...|
|subcategory|string|[subcategories list](#events-classification)|subclassification of the event...|
|description|string|(dynamic)|Free text characterising the report and should be used for human readable|
|timestamp|datetime(ISO8601)|(dynamic)|Event timestamp|
|source_key|string|["ip", "domain", "url", "email", "uri", "sample", "imei", "MAC", "phone number"]|....|
|source_value|string|(dynamic)|...|
|source_port|int|(dynamic)|-|
|source_asn|int|(dynamic)|Autonous System Number|
|destination_key|string|["ip", "domain", "url", "email", "uri", "sample", "imei"]|....|
|destination_value|string|(dynamic)|...|
|destination_port|int|(dynamic)|-|
|destination_asn|int|(dynamic)|Autonous System Number|
|transport_protocol|string|["tcp", "udp", "icmp"]|This field is used to give infroamtion about the attack for example attack by UDP...|
|protocol|string|["dns", "http, "ssh", etc..]|This field is used to give infroamtion about the attack for example attack though SSH|
|sample_hash|string|["md5", "sha512"]|Hash of the sample|
|sample_filename|string|string|Filename of the sample|

=
**To Remove:**
```
|confidence|string|[check sensors confidence values](http://nowhere.com)|MUST|TBD|Level of confidence in source **(this value should not exist because CCH is who can decide in the central point)**|
```

# Sensors Harmonization

### *Minimum Dataset*
**Perspective:**:

** Dataset **


Field|Defined Values| Example| Level Req.| Specific description|
|---|---|---|---|------|
|sensor|[sensor list](#sensor-identification)|"Horga"|MUST|\<descrever\>|
|category|[categories list](#events-classification)|"website"|MUST||
|subcategory|"bot"||MUST||
|description|"Bot (infected system) connected to C&C server."||MUST||
|timestamp|(dynamic)||MUST||
|source_key|"ip"|MUST||
|source_value|(dynamic)||MUST||
|source_port|(dynamic)||MAY||
|source_asn|(dynamic)||SHOULD||
|destination_key|"ip"||MUST||
|destination_value|(dynamic)||MUST||
|destination_port|(dynamic)||MAY||
|destination_asn|(dynamic)||SHOULD||
|protocol|(dynamic)|SHOULD||
|transport_protocol|(dynamic)||SHOULD||

=

### *Bot Detection Reports Fields Harmonization*

**Perspective:** Bot ip must be inserted in source_value and C&C ip must be inserted in destination_value.

**Dataset**

Field|Defined Values| Example| Level Req.| Specific description|
|---|---|---|---|------|
|sensor|[sensor list](#sensor-identification)|"Horga"|MUST|\<descrever\>|
|category|[categories list](#events-classification)|"website"|MUST||
|subcategory|"bot"||MUST||
|description|"Bot (infected system) connected to C&C server."||MUST||
|timestamp|(dynamic)||MUST||
|source_key|"ip"|MUST||
|source_value|(dynamic)||MUST||
|source_port|(dynamic)||MAY||
|source_asn|(dynamic)||SHOULD||
|destination_key|"ip"||MUST||
|destination_value|(dynamic)||MUST||
|destination_port|(dynamic)||MAY||
|destination_asn|(dynamic)||SHOULD||
|protocol|(dynamic)|SHOULD||
|transport_protocol|(dynamic)||SHOULD||


**JSON Example**

```
{
 "sensor": "Black-Holing",
 "category": "ddos",
 "subcategory": "bot",
 "description": "Bot (infected system) connected to C&C server.", 
 "timestamp": "2014-07-15T00:16:29+00:00",
 "source_key": "ip",
 "source_value": "192.135.6.215",
 "source_port": "53653",
 "source_asn": "1930",
 "destination_key": "ip",
 "destination_value": "192.80.6.215", 
 "destination_port": "994",
 "destination_asn": "19165",
 "transport_protocol": "udp"
}
```




### *C&C Detection Reports Fields Harmonization*

**Perspective:** C&C ip must be inserted in source_value.

**Dataset**

Field|Defined Values|Level Req.|Field description|
|---|---|---|---|
|sensor|[sensor list](#sensor-identification)|MUST|\<descrever\>|
|category|[categories list](#events-classification)|MUST||
|subcategory|"c&c"|MUST||
|description|"C&C server found."|MUST||
|timestamp|(dynamic)|MUST||
|source_key|"ip"|MUST||
|source_value|(dynamic)|MUST||
|source_port|(dynamic)|MAY||
|source_asn|(dynamic)|SHOULD||
|protocol|(dynamic)|SHOULD||
|transport_protocol|(dynamic)|SHOULD||


**JSON Example**

```
{
 "sensor": "DDoS Monitoring Tool",
 "category": "ddos",
 "subcategory": "c&c",
 "description": "C&C server found.", 
 "timestamp": "2014-07-15T00:16:29+00:00",
 "source_key": "ip",
 "source_value": "192.80.6.215",
 "source_port": "994",
 "source_asn": "19165",
 "transport_protocol": "udp"
}
```

# Specific categories
### *DDoS Reports Fields Harmonization*

#### Case: Report an Dos Attack.

**Perspective:** Source IP of attack must be inserted in source_value and 'destination IP' (victim) must be inserted in 'destination_value'.

**Dataset**

Field|Defined Values|Level Req.|Field description|
|---|---|---|---|
|sensor|["DDoS Monitoring Tool","Black-Holing", (...)] |MUST|\<descrever\>|
|category|"ddos"|MUST||
|subcategory|"flood"|MUST||
|timestamp|(dynamic)|MUST||
|description|"DoS Attack from source to destination."|MUST||
|source_key|"ip"|MUST||
|source_value|(dynamic)|MUST||
|source_port|(dynamic)|MUST||
|source_asn|(dynamic)|SHOULD||
|destination_key|"ip"|MUST||
|destination_value|(dynamic)|MUST||
|destination_port|(dynamic)|MUST||
|destination_asn|(dynamic)|MAY||
|transport_protocol|(dynamic)|MUST||


**JSON Example**

```
{
 "sensor": "DDoS Monitoring Tool",
 "category": "ddos",
 "subcategory": "flood",
 "timestamp": "2014-07-15T00:16:29+00:00",
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

=
### *WEBSITE Reports Fields Harmonization*

#### Case: Report a Malicious Website.

**Note:** TBD.

**Dataset**

Field|Defined Values|Level Req.|Field description|
|---|---|---|---|
|sensor|["initiative-S","DNS Traffic Sensor", "Skanna","Honeypot Sensor",(...)]|MUST|MUST|\<descrever\>|
|category|"website"|MUST||
|subcategory|"malicious content"|MUST||
|timestamp|(dynamic)|MUST||
|description|"Website found with malicious content."|MUST||
|source_key|"url"|MUST||
|source_value|(dynamic)|MUST||
|source_port|(dynamic)|MAY||
|source_asn|(dynamic)|SHOULD||
|protocol|"http"|MAY||
|transport_protocol|(dynamic)|MAY||


**JSON Example**

```
{
 "sensor": "Skanna",
 "category": "website",
 "subcategory": "malicious content",
 "timestamp": "2014-05-29T23:28:09+00:00",
 "description": "Website found with malicious content.", 
 "source_key": "url",
 "source_value": "https://xasdda.xxxxx.com/pub.php",
 "source_port": "443",
 "source_asn": "8982",
 "protocol": "http",
 "transport_protocol": "tcp"
}
```
=
#### Case: Report a Malware binary.

**Note:** TBD.

**Dataset**

Field|Defined Values|Level Req.|Field description|
|---|---|---|---|
|sensor|["initiative-S","Horga", "Skanna","Honeypot Sensor",(...)]|MUST|\<descrever\>
|category|"website"|MUST||
|subcategory|"malware"|MUST||
|timestamp|(dynamic)|MUST||
|description|"Website found with malware binary."|MUST||
|source_key|"sample"|MUST||
|source_value|(dynamic)|MUST||
|sample_hash|(dynamic)|MUST||
|sample_filename|(dynamic)|MUST||


**JSON Example**

```
{
 "sensor": "Horga",
 "category": "website",
 "subcategory": "malware",
 "timestamp": "2013-01-30T23:28:09+00:00",
 "description": "Website found with malware binary.", 
 "source_key": "sample",
 "source_value": "dGhpcyBpcyB0aGUgYmluYXJ5IHNhbXBsZSBlbmNvZGVk",
 "sample_hash": "dbd014125a4bad51db85f27279f1040a",
 "sample_filename": "best-antivirus.exe"
}
```
=
# Validar a partir daqui. Apenas estão as estruturas.
#### Case: Report a Vulnerable Website.
**Note:** TBD.

**Dataset**

Field|Defined Values|Level Req.|Field description|
|---|---|---|---|
|sensor|["initiative-S","Horga", "Skanna","Honeypot Sensor",(...)]|MUST|\<descrever\>
|category|"website"|MUST||
|subcategory|"vulnerable"|MUST||
|timestamp|(dynamic)|MUST||
|description|"Vulnerable website."|MUST||
|source_key|"url"|MUST||
|source_value|(dynamic)|MUST||
|sample_hash|(dynamic)|MUST||
|sample_filename|(dynamic)|MUST||

**JSON Example**

```
{
 "sensor": "Horga",
 "category": "website",
 "subcategory": "vulnerable",
 "timestamp": "2013-01-30T23:28:09+00:00",
 "description": "Vulnerable website.", 
 "source_key": "........",
 "source_value": "dGhpcyBpcyB0aGUgYmluYXJ5IHNhbXBsZSBlbmNvZGVk",
 "sample_hash": "dbd014125a4bad51db85f27279f1040a",
 "sample_filename": "best-antivirus.exe"
}
```
=
### *FastFlux Reports Fields Harmonization*
#### Case: Report a Fastflux malicious content.
**Note:** TBD.

**Dataset**



Field|Defined Values|Level Req.|Field description|
|---|---|---|---|
|sensor|["Passive dns sensor","DNS Traffic Sensor", "Flux Detect",(...)]|MUST|MUST|\<descrever\>|
|category|"fastflux"|MUST||
|subcategory|"malicious content"|MUST||
|timestamp|(dynamic)|MUST||
|description|"............."|MUST||
|source_key|"`domain`"|MUST||
|source_value|(dynamic)|MUST||
|source_port|(dynamic)|MAY||
|source_asn|(dynamic)|SHOULD||
|protocol|"http"|MAY||
|transport_protocol|(dynamic)|MAY||


**JSON Example**

```
{
 "sensor": "Flux Detec",
 "category": "fastflux",
 "subcategory": "malicious content",
 "timestamp": "2014-05-29T23:28:09+00:00",
 "description": "...........", 
 "source_key": "`domain`",
 "source_value": "........",
 "source_port": "443",
 "source_asn": "8982",
 "protocol": "http",
 "transport_protocol": "tcp"
}
```
=
### *Mobile Reports Fields Harmonization*
#### Case: Report a Malware binary.

**Note:** TBD.

**Dataset**

Field|Defined Values|Level Req.|Field description|
|---|---|---|---|
|sensor|["Suricata IDS","Conan mobile",(...)]|MUST|\<descrever\>
|category|"mobile"|MUST||
|subcategory|"malware"|MUST||
|timestamp|(dynamic)|MUST||
|description|"Mobile found with malware binary."|MUST||
|source_key|"sample"|MUST||
|source_value|(dynamic)|MUST||
|sample_hash|(dynamic)|MUST||
|sample_filename|(dynamic)|MUST||


**JSON Example**

```
{
 "sensor": "Conan mobile",
 "category": "mobile",
 "subcategory": "malware",
 "timestamp": "2013-01-30T23:28:09+00:00",
 "description": "mobile found with malware binary.", 
 "source_key": "sample",
 "source_value": "dGhpcyBpcyB0aGUgYmluYXJ5IHNhbXBsZSBlbmNvZGVk",
 "sample_hash": "dbd014125a4bad51db85f27279f1040a",
 "sample_filename": "best-antivirus.exe"
}
```

=
#### Case: Report a Malicious Content.

**Note:** TBD.

**Dataset**

Field|Defined Values|Level Req.|Field description|
|---|---|---|---|
|sensor|["Suricata IDS","Conan mobile",(...)]|MUST|MUST|\<descrever\>|
|category|"mobile"|MUST||
|subcategory|"malicious content"|MUST||
|timestamp|(dynamic)|MUST||
|description|"Mobile found with malicious content."|MUST||
|source_key|".........."|MUST||
|source_value|(dynamic)|MUST||
|source_port|(dynamic)|MAY||
|source_asn|(dynamic)|SHOULD||
|protocol|"......."|MAY||
|transport_protocol|(dynamic)|MAY||


**JSON Example**

```
{
 "sensor": "Suricata IDS",
 "category": "mobile",
 "subcategory": "malicious content",
 "timestamp": "2014-05-29T23:28:09+00:00",
 "description": "Mobile found with malicious content.", 
 "source_key": "...............",
 "source_value": "...................",
 "source_port": "443",
 "source_asn": "8982",
 "protocol": "..........",
 "transport_protocol": "........."
}
```
=

#### Case: Report a Event.

**Note:** TBD.

**Dataset**

Field|Defined Values|Level Req.|Field description|
|---|---|---|---|
|sensor|["Suricata IDS","Conan mobile",(...)]|MUST|MUST|\<descrever\>|
|category|"mobile"|MUST||
|subcategory|"event"|MUST||
|timestamp|(dynamic)|MUST||
|description|"......."|MUST||
|source_key|".........."|MUST||
|source_value|(dynamic)|MUST||
|source_port|(dynamic)|MAY||
|source_asn|(dynamic)|SHOULD||
|protocol|"......."|MAY||
|transport_protocol|(dynamic)|MAY||


**JSON Example**

```
{
 "sensor": "Suricata IDS",
 "category": "mobile",
 "subcategory": "event",
 "timestamp": "2014-05-29T23:28:09+00:00",
 "description": ".......", 
 "source_key": "...............",
 "source_value": "...................",
 "source_port": "443",
 "source_asn": "8982",
 "protocol": "..........",
 "transport_protocol": "........."
}
```
=
### *SPAM Reports Fields Harmonization*
#### Case: Report a Malware binary.

**Note:** TBD.

**Dataset**

Field|Defined Values|Level Req.|Field description|
|---|---|---|---|
|sensor|["Spamtrap","Spambot detector","Spam analysis tool","AHPS"(...)]|MUST|\<descrever\>
|category|"spam"|MUST||
|subcategory|"malware"|MUST||
|timestamp|(dynamic)|MUST||
|description|"Spam found with malware binary."|MUST||
|source_key|"sample"|MUST||
|source_value|(dynamic)|MUST||
|sample_hash|(dynamic)|MUST||
|sample_filename|(dynamic)|MUST||


**JSON Example**

```
{
 "sensor": "Spamtrap",
 "category": "spam",
 "subcategory": "malware",
 "timestamp": "2013-01-30T23:28:09+00:00",
 "description": "spam found with malware binary.", 
 "source_key": "sample",
 "source_value": "dGhpcyBpcyB0aGUgYmluYXJ5IHNhbXBsZSBlbmNvZGVk",
 "sample_hash": "dbd014125a4bad51db85f27279f1040a",
 "sample_filename": "best-antivirus.exe"
}
```

=
#### Case: Report a Malware content.

**Note:** TBD.

**Dataset**

Field|Defined Values|Level Req.|Field description|
|---|---|---|---|
|sensor|["Spamtrap","Spambot detector","Spam analysis tool","AHPS"(...)]|MUST|\<descrever\>
|category|"spam"|MUST||
|subcategory|"malicious content"|MUST||
|timestamp|(dynamic)|MUST||
|description|"Website found with malicious content."|MUST||
|source_key|"url"|MUST||
|source_value|(dynamic)|MUST||
|source_port|(dynamic)|MAY||
|source_asn|(dynamic)|SHOULD||
|protocol|"http"|MAY||
|transport_protocol|(dynamic)|MAY||


**JSON Example**

```
{
 "sensor": "Spamtrap",
 "category": "spam",
 "subcategory": "malicious content",
 "timestamp": "2014-05-29T23:28:09+00:00",
 "description": "spam found with malicious content.", 
 "source_key": "url",
 "source_value": "https://xasdda.xxxxx.com/pub.php",
 "source_port": "443",
 "source_asn": "8982",
 "protocol": "http",
 "transport_protocol": "tcp"
}
```

=
#### Case: Report a campaign
**Note:** TBD.

**Dataset**

Field|Defined Values|Level Req.|Field description|
|---|---|---|---|
|sensor|["Spamtrap","Spambot detector","Spam analysis tool","AHPS"(...)]|MUST|\<descrever\>
|category|"spam"|MUST||
|subcategory|"campaign"|MUST||
|timestamp|(dynamic)|MUST||
|description|"......."|MUST||
|source_key|"...."|MUST||
|source_value|(dynamic)|MUST||
|source_port|(dynamic)|MAY||
|source_asn|(dynamic)|SHOULD||
|protocol|"http"|MAY||
|transport_protocol|(dynamic)|MAY||


**JSON Example**

```
{
 "sensor": "Spamtrap",
 "category": "spam",
 "subcategory": "campaign",
 "timestamp": "2014-05-29T23:28:09+00:00",
 "description": "......", 
 "source_key": "...",
 "source_value": "https://xasdda.xxxxx.com/pub.php",
 "source_port": "443",
 "source_asn": "8982",
 "protocol": "http",
 "transport_protocol": "tcp"
}
```

=


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


