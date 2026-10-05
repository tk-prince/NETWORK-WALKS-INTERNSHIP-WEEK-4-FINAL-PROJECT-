# Mediroza General Hospital Penetration Testing Exercise

> **Authorised training environment only.** This repository documents an educational, black-box assessment performed for the Networkwalks internship exercise. Do not reuse the techniques, payloads, credentials, patient information, or target references against systems without explicit written permission.

## Overview

This submission records an assessment of the Mediroza General Hospital training environment. The assessment demonstrated a chain of weaknesses that allowed unauthorised access to confidential patient reports and pointed to a publicly exposed legacy database backup.

## Scope

| Item | Detail |
| --- | --- |
| Assessment type | Black-box penetration test and vulnerability assessment |
| Authorised target | `https://medirozahospital.com` |
| Constraints | Target domain only; no social engineering; no denial of service; no out-of-scope testing |
| Exercise milestones | Initial access, file recovery, data-exposure analysis, reporting |

## Key findings

| ID | Finding | Severity |
| --- | --- | --- |
| F-01 | Username enumeration in the patient portal | Medium |
| F-02 | SQL injection enabled authentication bypass | Critical |
| F-03 | Patient reports were accessible after bypass | High |
| F-04 | Report encryption used weak, guessable passwords | High |
| F-05 | PDF metadata disclosed an internal backup-location clue | Medium |
| F-06 | A legacy directory exposed a database backup through directory listing | Critical |
| F-07 | The backup contained confidential staff compensation and shareholder information in plaintext | Critical |

## Exposure chain

```text
robots.txt -> hidden patient portal -> account enumeration
             -> SQL injection -> report access -> weak PDF protection
             -> report metadata -> /old/ legacy directory -> database backup
             -> staff salaries + shareholder data
```


## Recommended remediation priorities

1. Remove public access to backups and disable directory listing immediately.
2. Replace vulnerable login queries with parameterised queries; rotate affected credentials and investigate access logs.
3. Move reports outside the web root and enforce server-side authorisation checks.
4. Replace weak PDF passwords with a secure delivery mechanism and remove unnecessary metadata.
5. Standardise authentication error responses to prevent account enumeration.

