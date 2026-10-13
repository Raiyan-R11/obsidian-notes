---
tags: [networking, concept]
created: 2026-10-13
updated: 2026-10-13
---

# DNS

Domain Name System: translates human-friendly hostnames into IP addresses.

## Terms

- **Domain registrar** — where a domain name is registered (e.g. Cloudflare)
- **DNS record** — a mapping entry; types include A, AAAA, CNAME, NS
- **Zone file** — contains the DNS records for a zone
- **Root** — the `.` at the end of a URL
- **NS (name server)** — resolves DNS queries; authoritative or non-authoritative
- **TLD** — top-level domain, e.g. `.com`
- **SLD** — second-level domain, e.g. `google.com`
- **FQDN** — fully qualified domain name
- **Zone apex** — top node of a namespace, e.g. `example.com`
- **Authoritative** — the customer can update the records

## Resolution flow (example.com)

1. Browser looks up `example.com`.
2. Local DNS server is queried; returns the IP if cached, else asks Root DNS.
3. Root DNS returns the `.com` TLD name server IP.
4. TLD DNS returns the `example.com` name server IP.
5. SLD DNS returns the `example.com` IP.
6. Local DNS server returns the IP to the browser.
7. Browser connects to the web server using that IP.

---

## Related
- [[Amazon Route 53]] — AWS's authoritative DNS service
- [[Route 53]] — source summary this page came from
