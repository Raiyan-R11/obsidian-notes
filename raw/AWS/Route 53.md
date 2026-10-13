DNS - Domain Name System
- translates human friendly hostnames into IP addresses

Domain Registrar - Cloudflare - register domain names
DNS records - different types - A,AAAA, etc
Zone files - contains DNS records
Root - . (dot) at the end of a URL
NS - resolves DNS queries - (Authoritative or Non-Authoritative)
TLD - Top Level Domain - .com
SLD - Second Level Domain - google.com
FQDN - Fully Qualified Domain Name
Protocol - HTTP / HTTPS

top node of a name space is called a Zone Apex - eg. example.com

How DNS works
1. Web Browser - search example.com
2. Local DNS Server queried - example.com? - if exists, returns IP - else, asks Root DNS
3. Root DNS Server - example.com? - returns .com NS IP 
4. TLD DNS Server - example.com? - returns example.com NS IP
5. SLD DNS Server - example.com? - returns example.com IP
6. Local DNS Server - returns example.com IP to Web Browser
7. example.com Web Server browsed using IP

Authoritative - allows the customer to update DNS records

Route 53 **record** contains:
* Domain/subdomain name
* Record Type
* Routing Policy
* TTL - amount of time a record can be cached at DNS resolvers

Record Types:
A - maps to IPv4 address
AAAA - maps to IPv6 address
CNAME - maps to a hostname that must result a A or AAAA 
NS - Name Servers for the **Hosted Zone** - responds to DNS queries for my hosted zone

Hosted Zones:
A container that **defines** how to route requests to your domains and its subdomains.
Public Hosted Zones: Allows anyone from the public internet to query records.
	Contains records on how to route traffic on the internet.
Private Hosted Zone:  Allows users within private resources such as a VPC to query  records.
	Contains records on how to route traffic within one or more VPCs

TTL
Time To Live for a record to be cached on a clients device, before route 53 is queried again.

 CNAME vs Alias
	CNAME: maps hostname to a hostname
		! cannot map to a root domain such as example.com. 
		only **something.example.com allowed**
	Alias: maps hostname to an AWS resource - A / AAAA record type
		CAN be mapped to a root domain or non-root domain
		Free
		Native health check --> "Evaluate Target Health" checkbox - uses the AWS resource's own health (no path sent by Route 53)
		Available targets: ELB , Amazon CloudFront , API Gateway , S3 Website , VPC interface endpoints etc. 
			! cannot set an alias record for EC2 DNS

Routing policies
	**Simple** - multiple IPs returned - random chosen by client
	**Weighted** - assign a weight (0-255) to a EC2 IP. % of traffic is routed based on weight. 100 , 60 , 40 --> 50% , 30% , 20% traffic routed
	**Latency** - users routed based on latency (faster reponse times)
	


Health Checks
	Route 53 health checkers sit OUTSIDE the VPC --> can only reach PUBLIC endpoints
	Types:
	**Endpoint** - monitors an IP / domain name
		protocol: HTTP / HTTPS / TCP, port, interval, failure threshold
		path - optional, default "/" - HTTP(S) 2xx / 3xx = healthy
		string matching - first 5120 bytes of the response
		public resources only
	**CloudWatch alarm** - for PRIVATE resources
		create a CloudWatch alarm on a metric --> health check follows the alarm state
		no path involved
	**Calculated** - combines other health checks (AND / OR)
	Alias record - "Evaluate Target Health" - free, no separate health check
		not available for every target type (eg. S3 website, VPC interface endpoints) - check the target

--
Costs 
$0.5 per month for a hosted zone
charged per request/query to Route 53 DNS (higher TTL , means IP is cached on client, less cost)


