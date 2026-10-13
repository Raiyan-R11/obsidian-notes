---
tags: [aws, dns, source]
created: 2026-10-13
updated: 2026-10-13
source: raw/AWS/Route 53.md
---

# Route 53 (source summary)

Summary of my AWS study note on DNS fundamentals and Amazon Route 53.

## What the note covers

- DNS basics: hostname → IP translation, registrar, zone files, root/TLD/SLD, FQDN, zone apex
- The 7-step DNS resolution flow (Local → Root → TLD → SLD → back to browser)
- Route 53 record anatomy: name, type, routing policy, TTL
- Record types: A, AAAA, CNAME, NS
- Hosted zones: public vs private
- CNAME vs Alias
- Routing policies: Simple, Weighted (only these two so far)
- Costs: $0.50/month per hosted zone + per-query charges

## Where it landed

- [[DNS]] — concepts and resolution flow
- [[Amazon Route 53]] — service details, records, hosted zones, Alias, routing, costs

## Gaps in the note

- No mention of global vs regional scope (added to [[Amazon Route 53]] from general knowledge, flagged there)
- Remaining routing policies not yet noted (Latency, Failover, Geolocation, Geoproximity, IP-based, Multi-value)
- Health checks only touched on via Alias

---

## Related
- [[Amazon Route 53]] — main entity page
- [[DNS]] — underlying concept page
