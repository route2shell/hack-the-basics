# Service Enrichment Playbook - Module 02

---

> **Playbook Role**
>
> Use this when moving from open ports to service clues that Module 03 can interpret.

Service enrichment asks:

> What appears to be behind the open port, and what clue should be preserved for the next workflow?

---

## First Questions

Ask:

1. Which ports were observed open?
2. Which host is most worth enriching first?
3. Will version detection answer the next question?
4. Would a targeted script add useful context?
5. Where will output be saved?

---

## Commands

```bash
nmap -sV -Pn -p <open-ports> -oA "$M2SCAN"/<host>-version-YYYY-MM-DD <target>
nmap -sV -sC -Pn -p <open-ports> -oA "$M2SCAN"/<host>-defaultscripts-YYYY-MM-DD <target>
```

Focused examples:

```bash
nmap --script http-title,ssl-cert -p 80,443 -oA "$M2SCAN"/meta-web-focused-YYYY-MM-DD 192.168.57.25
nmap --script smb-os-discovery,smb-security-mode -p 445 -oA "$M2SCAN"/dc01-smb-focused-YYYY-MM-DD 192.168.57.10
nmap --script ldap-rootdse -p 389 -oA "$M2SCAN"/dc01-ldap-rootdse-YYYY-MM-DD 192.168.57.10
```

---

## Interpretation

Service detection may reveal:

- product names
- versions
- hostnames
- titles
- certificates
- protocol capabilities
- OS hints
- script-generated context

Treat these as clues, not final truth.

Example:

```text
Apache-like HTTP title observed on 192.168.57.25. This supports web follow-up but does not identify the full application or vulnerability state.
```

---

## Strong Note Example

```text
Observed:
Service enrichment on 192.168.57.10 shows DNS, Kerberos, LDAP, and SMB-related services.

Inference:
The host likely has Windows identity infrastructure relevance.

Validation needed:
Module 03 should footprint DNS, LDAP, Kerberos, and SMB roles before making stronger host-role claims.

Evidence path:
assessment-workspace/02-evidence/scans/m02/dc01-service-enriched-2026-05-04.nmap
```

