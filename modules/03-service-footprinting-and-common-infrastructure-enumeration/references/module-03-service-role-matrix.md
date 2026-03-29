# Module 03 Service Role Matrix

---

> **📝 Worksheet Purpose**
>
> Use this matrix to translate visible services into role, trust, data, and follow-up meaning.

| Service family | Likely environment role | High-value clues to capture | Natural next workflow |
|---|---|---|---|
| DNS / naming | naming and infrastructure mapping | hostnames, domains, records | recon, identity context |
| LDAP / Kerberos | centralized identity | naming contexts, realms, trust clues | credentials, Windows, AD |
| SMB / NFS / FTP | storage and sharing | shares, exports, paths, auth posture | service follow-up, creds, foothold prep |
| SMTP / IMAP / POP3 | messaging | mail hosts, auth posture, TLS clues | credential and service triage |
| MySQL / MSSQL / Oracle | data and app back-end | version, instance, app role | common-service testing, app context |
| SNMP / IPMI | monitoring and device control | device identity, topology, admin value | infrastructure triage |
| SSH / WinRM / RDP | administration and remote access | host role, auth context, management value | service attack paths, foothold planning |

---

## Design Notes

This matrix should eventually be paired with worked examples and visual host-role diagrams.
