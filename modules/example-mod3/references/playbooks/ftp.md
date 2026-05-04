# FTP Playbook - Module 03

---

> **Playbook Role**
>
> Use this when FTP appears and you need to determine what the service reveals without turning Module 03 into exploitation or file looting.

FTP matters because it may expose file transfer behavior, software banners, anonymous access, readable directories, writable directories, or operational artifacts.

The first question is:

> Does this FTP service reveal identity, files, permissions, or host role in a safe first pass?

---

## First-Pass Questions

Ask:

1. What banner or software clue appears?
2. Is anonymous login allowed?
3. If anonymous login works, what directories are visible?
4. Are files readable?
5. Is writing allowed?
6. Do names suggest backups, web roots, users, deployments, or configuration?
7. Does this route to credentials, web, service attack, or foothold preparation later?

---

## Commands

```bash
nmap -sV -p 21 <target>
nc -nv <target> 21
ftp <target>
```

Inside FTP:

```text
anonymous
ls
pwd
get <file>
quit
```

Only download files that are clearly part of the lab and relevant to the task. Preserve evidence paths and avoid destructive actions.

---

## Interpretation

### Banner only

A banner may reveal software, version, or host naming. That is useful but usually not enough by itself.

### Anonymous login succeeds

This raises priority because the service allows unauthenticated interaction. The next question is whether the visible files or directories reveal anything meaningful.

### Writable location appears

Writable FTP is important, but Module 03 should still be careful. The finding may route into Module 09 or Module 10 later, especially if it can affect web content or execution paths.

### No anonymous access

That does not make FTP irrelevant. It may become useful after credentials exist, especially if credential reuse appears in Module 06.

---

## Strong Note Example

```text
Observed:
21/tcp open on 192.168.57.25. FTP banner returned service software. Anonymous login was accepted and directory listing showed public files.

Inference:
FTP provides unauthenticated file-surface visibility on the Linux target. This may reveal operational files or route into later service-specific testing.

Validation needed:
Record exact filenames and permissions. Avoid writing files unless a later scoped lab requires it.

Next workflow:
Module 09 if service weakness validation is needed; Module 10 only if a validated path leads to controlled access.
```

