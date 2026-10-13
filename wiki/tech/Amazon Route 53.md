---
tags: [aws, dns, service]
created: 2026-10-13
updated: 2026-10-13
---

# Amazon Route 53

AWS's authoritative DNS service: lets you manage records and route traffic for your domains.

## Scope

- **Global service** — no region to choose for hosted zones or records.
- Route 53 **Resolver** (VPC DNS resolver, inbound/outbound endpoints) is **regional**.
- Health checks and routing targets can point at region-specific resources; the records themselves stay global.

> [!note] Source
> Scope is not in [[Route 53]]; added from general AWS knowledge on 2026-10-13. Verify against the AWS course slides when ingested.

## Record contents

- Domain / subdomain name
- Record type
- Routing policy
- TTL — how long resolvers/clients may cache the record

## Record types

| Type | Maps to |
| ---- | ------- |
| A | IPv4 address |
| AAAA | IPv6 address |
| CNAME | a hostname that must ultimately resolve to an A or AAAA |
| NS | name servers for the hosted zone; answer DNS queries for it |

## Hosted zones

A container that defines how to route requests for a domain and its subdomains.

- **Public** — anyone on the internet can query; routes internet traffic
- **Private** — only resources inside one or more VPCs can query; routes traffic within VPCs

## CNAME vs Alias

- **CNAME** — hostname → hostname
    - Cannot be used at the root domain (`example.com`); only `something.example.com`
- **Alias** — hostname → AWS resource (A / AAAA)
    - Works at root and non-root
    - Free
    - Native health check
    - Targets: ELB, CloudFront, API Gateway, S3 website, VPC interface endpoints, etc.
    - Cannot target an EC2 DNS name

## Routing policies

- **Simple** — multiple IPs returned; client picks one at random
- **Weighted** — weight 0–255 per record; traffic split by share of total
    - Example: 100 / 60 / 40 → 50% / 30% / 20%

## Costs

- $0.50 per month per hosted zone
- Charged per DNS query; higher TTL → more client caching → fewer queries → lower cost

---

## Related
- [[DNS]] — underlying concepts and resolution flow
- [[Route 53]] — source summary
