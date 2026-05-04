# DNS and Naming Playbook - Module 03

---

> **Playbook Role**
>
> Use this when DNS or naming clues appear and you need to turn records into host-role and environment context.

DNS matters because naming is how environments describe themselves. A DNS service may reveal domains, host roles, mail routing, service records, and internal naming conventions.

The first question is:

> What names does this environment use to describe its systems?

---

## First-Pass Questions

Ask:

1. Which host appears to provide DNS?
2. Does reverse lookup reveal useful hostnames?
3. Is there a known lab or internal domain?
4. What records can be queried safely?
5. Do names suggest identity, mail, web, admin, or database roles?
6. Do DNS clues explain other exposed services?

---

## Commands

```bash
host <ip>
dig @<dns-server> -x <ip>
dig @<dns-server> <domain> A
dig @<dns-server> <domain> NS
dig @<dns-server> <domain> MX
dig @<dns-server> <domain> SRV
```

Zone transfer checks should be scoped and deliberate:

```bash
dig @<dns-server> axfr <domain>
```

Do not brute-force names in Module 03 unless the lab specifically asks for it. Heavy discovery belongs in later recon or fuzzing workflows.

---

## Interpretation

### PTR names

PTR records can validate that an IP belongs to a host with a meaningful name. A name like `dc01`, `ws01`, `files01`, `mail01`, or `vpn01` changes host-role reasoning.

### NS and SOA records

These can identify which server is authoritative for a zone. That matters when deciding whether a host is simply using DNS or actually responsible for naming.

### MX records

MX records route into messaging and identity context. They may tell you where mail services live, which hostnames matter, or whether a third-party provider handles mail.

### SRV records

SRV records can expose service location for directory and identity systems. In Windows environments, they often become especially useful later in AD work.

---

## Strong Note Example

```text
Observed:
192.168.57.10 answers DNS queries and reverse lookup returns a domain-oriented hostname. LDAP and Kerberos are also exposed on the same host.

Inference:
DNS strengthens the hypothesis that this host participates in identity infrastructure rather than being a random web or file server.

Validation needed:
Query naming context through LDAP and correlate with SMB/domain strings.

Next workflow:
Module 03 service triage now; Module 14 AD reasoning later.
```

