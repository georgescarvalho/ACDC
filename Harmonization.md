# Dictionary

<a name="sensor-identification"></a>
### *Sensor Identification*
|Category|Sensor|Entity|
|---|---|---|
|ddos|DDoS Monitoring Tool|IF-IS|
|ddos|Black-Holing| DE-CIX |
|ddos|(...) | (...)|
||||
|website|Initiative-S|ECO|
|website|Horga|ISCTI|
|website|Skanna|INTECO|
|website|Honeypot Sensor|CARNET|
|website| (...) | (...)|
||||
|fastflux|Passive DNS Sensor| CARNET|
|fastflux|DNS Traffic Sensor| ATOS|
|fastflux|Flux Detect|INTECO|
|fastflux| (...) | (...)|
||||
|mobile|Suricata IDS|XLAB|
|mobile|Conan Mobile|INTECO|
|mobile| (...) | (...)|
||||
|spam|Spamtrap|CARNET|
|spam|Spambot Detector|TID|
|spam|Spam Analysis Tool|CERT-RO|
|spam|AHPS|ATOS|
|spam| (...) | (...)|

<a name="events-classification"></a>
### *Events Classification*

|Category|SubCategory|
|---|---|
|ddos|flood|
|ddos|bot|
|ddos|c&c|
|||
|website|malware|
|website|malicious content|
|website|vulnerable|
|website|bot|
|website|c&c|
|||
|fastflux|malicious content|
|fastflux|bot|
|fastflux|c&c|
|||
|mobile|malware|
|mobile|malicious content|
|mobile|SMS Hijack|
|mobile|MAC Changed (FIXME)|
|mobile|IMEI Changed (FIXME)|
|mobile|bot|
|mobile|c&c|
|||
|spam|malware|
|spam|malicious content|
|spam|campaign|
|spam|bot|
|spam|c&c|



<a name="fields-list"></a>
### *Fields list*

**Description:** this table present all fields used by all sensors to define events.FIXME


|Field|Format|Defined Values|Field Description|Example|
|---|---|---|-----------|-----------|
|version|string|(dynamic)|The version number of the data format used for the report|"acdc-sensors-1.0"|
|sensor|string|[sensor list](#sensor-identification)|sensor name...|"Spambot Detector"|
|category|string|[categories list](#events-classification)|classification of the event...|"spam"|
|subcategory|string|[subcategories list](#events-classification)|subclassification of the event...|"bot"|
|description|string|(dynamic)|Free text characterising the report and should be used for human readable|"Bot (infected system) connected to C&C server."|
|timestamp|datetime(ISO8601)|(dynamic)|Event timestamp|"2014-07-15T00:16:29+00:00"|
|confidence_level|"string"|(dynamic)|FIXME|FIXME|
|source_key|string|["ip", "domain", "url", "email", "uri", "sample", "imei", "MAC", "phone number"]|Type of the reported object|"ip"|
|source_value|string|(dynamic)|The identifier (value) of the reported object|"8.8.8.8"|
|source_port|int|(dynamic)|FIXME|6375|
|source_asn|int|(dynamic)|Autonous System Number|5454|
|destination_key|string|["ip", "domain", "url", "email", "uri", "sample", "imei"]|FIXME|"ip"|
|destination_value|string|(dynamic)|FIXME|"8.8.4.4"|
|destination_port|int|(dynamic)|FIXME|80|
|destination_asn|int|(dynamic)|Autonous System Number|FIXME|5656|
|transport_protocol|string|["tcp", "udp", "icmp"]|This field is used to give infroamtion about the attack for example attack by UDP...FIXME|"tcp"|
|protocol|string|["dns", "http, "ssh", etc..]|This field is used to give infroamtion about the attack for example attack though SSH|"http"|
|sample_hash|string (SHA2)|(dynamic)|Hash of the sample|"f533383177f4e46605e5f30df13f8a2d"|
|sample_filename|string|(dynamic)|Filename of the sample|"antivirus.exe"|
|sample_binary|string (base64)|(dynamic)|FIXME|"0ibfLtDID2Rou944U9O72Jq0xLNsoyFa3+HmeglE2BsTJSTaISuzxLe"|
|campaign|"string"|(dynamic)|The name or identifier of the associated campaign|"Energy Safe Products"|
|log|base64|(dynamic)|FIXME|"dGhpcyBpcyBhIGxvZyBsaW5lCg=="|
|cwe|"string"|(dynamic)|The cwe associated to the vulnerability found|"CWE-89"|
|cve|"string"|(dynamic)|The cve associated to the vulnerability found|"CVE-2014-1849"|
|email_subject|"string"|(dynamic)|The subject of the spam message sent|"Buy new security products"|
|email_body|"string"|(dynamic)|The body of the spam message sent|"Content-Type: text/html; charset=UTF-8 Content-Transfer-Encoding: 7bit ..."|
|email_header|"string"|(dynamic)|The header of the spam message sent|"Return-Path: zzzzz@gmail.com X-Original-To: ..."|


# Sensors Harmonization

**Considerations:** all harmonization for all sensores must follow this document. In the next sections is present the minimum requirements for each case/scenario but if a sensor can fill more fields from harmonization, its possible to add that too but the fiels will still be optionals (SHOULD/MAY). FIXME

## Minimum Dataset

**Considerations** this minimum dataset MUST be applied to all scenarios. FIXME

**Dataset:**

**FIXME:** como melhorar a apresentacao desta tabela

|Field|
|---|
|[sensor](#fields-list)|
|[category](#fields-list)|
|[subcategory](#fields-list)|
|[description](#fields-list)|
|[timestamp](#fields-list)|
|[source_key](#fields-list)|
|[source_value](#fields-list)|

## *Commun / transversal Dataset*

### Bot Dataset

**Perspective:** Bot ip must be inserted in source_value and C&C ip must be inserted in destination_value.

**Dataset:**

Field|Defined Values| Level Req.| Specific description|
|---|---|---|---|------|
|sensor|[sensor list](#sensor-identification)|MUST|The sensor used to send bot data. Must be selected from "Sensor Identification" list|
|category|[categories list](#events-classification)|MUST|The category of sensor. Must be selected from "Events Classification" list|
|subcategory|"bot"|MUST|The category of the report. This links the report to one of ACDC's schemata. Must be selested from "Events Classification" list|
|description|"Bot (infected system) connected to C&C server."|MUST|Little description of the event. This is a free text field characterising the report that should be used for a human readable description rather than for automatic processin|
|timestamp|(dynamic)|MUST|The timestamp when the reported observation was detected|
|source_key|"ip"|MUST|\<descrever\>|
|source_value|(dynamic)|MUST|\<descrever\>|
|destination_key|"ip"|MUST|\<descrever\>|
|destination_value|(dynamic)|MUST|\<descrever\>|
|protocol|(dynamic)|SHOULD|\<descrever\>|
|transport_protocol|(dynamic)|SHOULD|\<descrever\>|
|source_asn|(dynamic)|SHOULD|\<descrever\>|
|destination_asn|(dynamic)|SHOULD|\<descrever\>|


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
 "source_asn": "1930",
 "destination_key": "ip",
 "destination_value": "192.80.6.215", 
 "destination_asn": "19165",
 "protocol": "dns",
 "transport_protocol": "udp"
}
```


### *C&C Detection Reports Fields Harmonization*

**Perspective:** C&C ip must be inserted in source_value.

**Dataset:**

Field|Defined Values|Level Req.|Specific description|
|---|---|---|---|---|
|sensor|[sensor list](#sensor-identification)|MUST|The sensor used to send C&C data. Must be selected from "Sensor Identification" list|
|category|[categories list](#events-classification)|MUST|\<descrever\>|
|subcategory|"c&c"|MUST|\<descrever\>|
|description|"C&C server found."|MUST|\<descrever\>|
|timestamp|(dynamic)|MUST|The timestamp when the reported observation was detected|
|source_key|"ip"|MUST|\<descrever\>|
|source_value|(dynamic)|MUST|\<descrever\>|
|source_asn|(dynamic)|SHOULD|\<descrever\>|
|protocol|(dynamic)|SHOULD|\<descrever\>|
|transport_protocol|(dynamic)|SHOULD|\<descrever\>|


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
 "source_asn": "19165",
 "protocol": "http",
 "transport_protocol": "tcp"
}
```

## Specific categories
### *DDoS Reports Fields Harmonization*

#### Case: Report an Dos Attack.

**Perspective:** Source IP of attack must be inserted in source_value and 'destination IP' (victim) must be inserted in 'destination_value'.

**Dataset**

Field|Defined Values|Level Req.|Specific description|
|---|---|---|---|
|sensor|["DDoS Monitoring Tool","Black-Holing", (...)]|MUST|The sensor used to send DDOS data. Must be selected from "Sensor Identification" list|
|category|"ddos"|MUST|\<descrever\>|
|subcategory|"flood"|MUST|\<descrever\>|
|timestamp|(dynamic)|MUST|The timestamp when the reported observation was detected|
|description|"DoS Attack from source to destination."|MUST|\<descrever\>|
|source_key|"ip"|MUST|\<descrever\>|
|source_value|(dynamic)|MUST|\<descrever\>|
|source_port|(dynamic)|MUST|\<descrever\>|
|destination_key|"ip"|MUST|\<descrever\>|
|destination_value|(dynamic)|MUST|\<descrever\>|
|destination_port|(dynamic)|MUST|\<descrever\>|
|transport_protocol|(dynamic)|MUST|\<descrever\>|
|source_asn|(dynamic)|SHOULD|\<descrever\>|


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
 "destination_key": "ip",
 "destination_value": "192.80.6.215", 
 "destination_port": "22",
 "transport_protocol": "udp",
  "source_asn": "1930"
}
```


### *WEBSITE Reports Fields Harmonization*

#### Case: Report a Malicious Website.

**Note:** FIXME.

**Dataset**

Field|Defined Values|Level Req.|Field description|
|---|---|---|---|
|sensor|["initiative-S","DNS Traffic Sensor", "Skanna","Honeypot Sensor",(...)]|MUST|The sensor used to send malicious website data. Must be selected from "Sensor Identification" list|
|category|"website"|MUST|.......|
|subcategory|"malicious content"|MUST|......|
|timestamp|(dynamic)|MUST|The timestamp when the reported observation was detected|
|description|"Website found with malicious content."|MUST|....|
|source_key|"url"|MUST|......|
|source_value|(dynamic)|MUST|.....|
|source_asn|(dynamic)|SHOULD|.....|


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

**Note:** FIXME.

**Dataset**

Field|Defined Values|Level Req.|Field description|
|---|---|---|---|
|sensor|["initiative-S","Horga", "Skanna","Honeypot Sensor",(...)]|MUST|The sensor used to send malware binary data. Must be selected from "Sensor Identification" list|
|category|"website"|MUST|...|
|subcategory|"malware"|MUST|...|
|timestamp|(dynamic)|MUST|The timestamp when the reported observation was detected|
|description|"Website found with malware binary."|MUST|...|
|source_key|"sample"|MUST|...|
|source_value|(dynamic)|MUST|...|
|sample_hash|(dynamic)|MUST|...|
|sample_filename|(dynamic)|MUST|...|


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
**Note:** FIXME.

**Dataset**

Field|Defined Values|Level Req.|Specific description|
|---|---|---|---|
|sensor|["initiative-S","Horga", "Skanna","Honeypot Sensor",(...)]|MUST|The sensor used to send vulnerable website data. Must be selected from "Sensor Identification" list|
|category|"website"|MUST|...|
|subcategory|"vulnerable"|MUST|...|
|timestamp|(dynamic)|MUST|The timestamp when the reported observation was detected|
|description|"Vulnerable website."|MUST|...|
|source_key|"url"|MUST|...|
|source_value|(dynamic)|MUST|...|
|sample_hash|(dynamic)|MUST|...|
|sample_filename|(dynamic)|MUST|...|

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
**Note:** FIXME.

**Dataset**



Field|Defined Values|Level Req.|Field description|
|---|---|---|---|
|sensor|["Passive dns sensor","DNS Traffic Sensor", "Flux Detect",(...)]|MUST|MUST|The sensor used to send fastflux malicious content data. Must be selected from "Sensor Identification" list|
|category|"fastflux"|MUST|...|
|subcategory|"malicious content"|MUST|...|
|timestamp|(dynamic)|MUST|The timestamp when the reported observation was detected|
|description|"............."|MUST|...|
|source_key|"domain"|MUST|...|
|source_value|(dynamic)|MUST|...|
|source_asn|(dynamic)|SHOULD|...|



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
 "source_asn": "8982"

}
```
=
### *Mobile Reports Fields Harmonization*
#### Case: Report a Malware binary.

**Note:** FIXME.

**Dataset**

Field|Defined Values|Level Req.|Field description|
|---|---|---|---|
|sensor|["Suricata IDS","Conan mobile",(...)]|MUST|The sensor used to send mobile malware binary data. Must be selected from "Sensor Identification" list|
|category|"mobile"|MUST|...|
|subcategory|"malware"|MUST|...|
|timestamp|(dynamic)|MUST|The timestamp when the reported observation was detected|
|description|"Mobile found with malware binary."|MUST|...|
|source_key|"sample"|MUST|...|
|source_value|(dynamic)|MUST|...|
|sample_hash|(dynamic)|MUST|...|
|sample_filename|(dynamic)|MUST|...|


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

**Note:** FIXME.

**Dataset**

Field|Defined Values|Level Req.|Field description|
|---|---|---|---|
|sensor|["Suricata IDS","Conan mobile",(...)]|MUST|MUST|The sensor used to send mobile malicious content data. Must be selected from "Sensor Identification" list|
|category|"mobile"|MUST|...|
|subcategory|"malicious content"|MUST|...|
|timestamp|(dynamic)|MUST|The timestamp when the reported observation was detected|
|description|"Mobile found with malicious content."|MUST|...|
|source_key|".........."|MUST|...|
|source_value|(dynamic)|MUST|...|
|source_asn|(dynamic)|SHOULD|...|



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
 "source_asn": "8982"

}
```
=


=
### *SPAM Reports Fields Harmonization*
#### Case: Report a Malware binary.

**Note:** FIXME.

**Dataset**

Field|Defined Values|Level Req.|Field description|
|---|---|---|---|
|sensor|["Spamtrap","Spambot detector","Spam analysis tool","AHPS"(...)]|MUST|The sensor used to send spam malware binary data. Must be selected from "Sensor Identification" list|
|category|"spam"|MUST|...|
|subcategory|"malware"|MUST|...|
|timestamp|(dynamic)|MUST|The timestamp when the reported observation was detected|
|description|"Spam found with malware binary."|MUST|...|
|source_key|"sample"|MUST|...|
|source_value|(dynamic)|MUST|...|
|sample_hash|(dynamic)|MUST|...|
|sample_filename|(dynamic)|MUST|...|


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

**Note:** FIXME.

**Dataset**

Field|Defined Values|Level Req.|Field description|
|---|---|---|---|
|sensor|["Spamtrap","Spambot detector","Spam analysis tool","AHPS"(...)]|MUST|The sensor used to send spam malware content data. Must be selected from "Sensor Identification" list|
|category|"spam"|MUST|...|
|subcategory|"malicious content"|MUST|...|
|timestamp|(dynamic)|MUST|The timestamp when the reported observation was detected|
|description|"Website found with malicious content."|MUST|...|
|source_key|"url"|MUST|...|
|source_value|(dynamic)|MUST|...|
|source_asn|(dynamic)|SHOULD|...|


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
 "source_asn": "8982"

}
```

=
#### Case: Report a campaign
**Note:** FIXME.

**Dataset**

Field|Defined Values|Level Req.|Field description|
|---|---|---|---|
|sensor|["Spamtrap","Spambot detector","Spam analysis tool","AHPS"(...)]|MUST|\<descrever\>
|category|"spam"|MUST|...|
|subcategory|"campaign"|MUST|...|
|timestamp|(dynamic)|MUST|The timestamp when the reported observation was detected|
|description|"......."|MUST|...|
|source_key|"...."|MUST|...|
|source_value|(dynamic)|MUST|...|
|source_asn|(dynamic)|SHOULD|...|


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
 "source_asn": "8982"

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


