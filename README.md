# Penetration Testing Report — Mediroza General Hospital

| Project Information | Details |
| :--- | :--- |
| **Organization** | NetworkWalks |
| **Prepared by** | Atharv Shinde |
| **Target** | `https://medirozahospital.com` |
| **Assessment Type** | Black-box penetration testing |
| **Assessment Period** | 6 days |
| **Report Date** | 26 November 2026 |

---

## Table of Contents
1. [Executive Summary](#1-executive-summary)
2. [Scope and Rules of Engagement](#2-scope-and-rules-of-engagement)
3. [Methodology](#3-methodology)
4. [Tools and Testing Environment](#4-tools-and-testing-environment)
5. [Findings and Evidence](#5-findings-and-evidence)
   - [5.1 M1 — Initial Access](#51-m1--initial-access)
   - [5.2 M2 — Data Extraction and Password-Hash Assessment](#52-m2--data-extraction-and-password-hash-assessment)
   - [5.3 M3 — Data Exposure Assessment](#53-m3--data-exposure-assessment)
   - [5.4 M4 — Reporting and Retesting](#54-m4--reporting-and-retesting)
6. [Risk Rating Summary](#6-risk-rating-summary)
7. [Recommendations and Remediation](#7-recommendations-and-remediation)
8. [Limitations](#8-limitations)
9. [Conclusion](#9-conclusion)

---

## 1. Executive Summary

A black-box security assessment was carried out as part of the **NetworkWalks Cybersecurity and Penetration Testing** program. The assessment focused on the public-facing Mediroza General Hospital web application and the milestones defined in the project brief: **M1 — Initial Access**, **M2 — Data Extraction**, **M3 — Data Exposure**, and **M4 — Reporting**.

The tester reports having collected initial-access and enumeration scan evidence, three PDF artifacts associated with the exercise, and password-hash cracking evidence showing recovery of password values. The exact access path, authorization context for the PDF artifacts, and the contents and sensitivity classification of those artifacts must be validated against the original evidence before final submission.

> **Disclaimer:** No conclusion is made in this report that a SQL injection vulnerability, authentication bypass, patient-data exposure, or database-backup exposure was confirmed unless the corresponding request/response evidence and scope authorization are attached and reviewed. M3 remains pending where no direct, authorized evidence of exposed database or business records has been supplied.

---

## 2. Scope and Rules of Engagement

| Item | Description |
| :--- | :--- |
| **Client / Scenario** | Mediroza General Hospital |
| **Target Domain** | `https://medirozahospital.com` |
| **Assessment Type** | Black-box web application assessment |
| **In-Scope Assets** | Only assets explicitly listed in the written authorization and project rules of engagement. |
| **Out-of-Scope Activities** | Denial-of-service, social engineering, testing third-party systems, and access to real patient or employee information without explicit written approval. |
| **Authorization** | `[Insert authorization reference, date, approved testing window, and permitted techniques.]` |
| **Testing Period** | `[Insert actual start and end dates.]` |

The assessment must remain within the approved target and testing window. The existence of a general project brief does not automatically authorize accessing, copying, decrypting, or retaining real patient records, staff salary information, shareholder records, or other confidential data. Where such information is encountered unexpectedly, testing should stop at the minimum proof necessary and the issue should be reported through the approved channel.

---

## 3. Methodology

* **Reconnaissance:** Review publicly visible pages, navigation, and approved entry points; record target information and timestamps.
* **Enumeration:** Review the scan and enumeration outputs already collected within the authorized scope. Record tool names, options, target, time, and result summary.
* **Initial-Access Assessment:** Document the exact authentication or access-control behavior demonstrated by the supplied evidence. Do not infer a successful bypass from a submitted payload alone.
* **File and Password Assessment:** Work only with instructor-provided or explicitly authorized test PDFs. Record file metadata, hash-extraction method, cracking result, and validation outcome without publishing passwords or raw hashes.
* **Data-Exposure Assessment:** Assess only approved test directories and synthetic backup/database material. Do not retrieve real patient, HR, or shareholder data.
* **Reporting:** Correlate each claim with evidence, assign a defensible risk rating, and provide remediation guidance.

---

## 4. Tools and Testing Environment

| Tool / Evidence Source | Purpose | Details to Complete |
| :--- | :--- | :--- |
| **Browser / Developer Tools** | Review public pages, request metadata, and response headers. | `[Browser/version and capture timestamps]` |
| **Enumeration Scanner** | Identify in-scope paths or services from the supplied scan evidence. | `[Exact tool, version, command/options, and scan file]` |
| **Kali Linux** | Testing environment for approved security assessment tasks. | `[Version / VM details]` |
| **PDF Hash Extraction Utility** | Extract a test-file hash representation for password-strength assessment. | `[Exact tool and version]` |
| **John the Ripper / Hashcat** | Perform an offline dictionary assessment against authorized test-file hashes. | `[Tool/version, mode, wordlist source, and final status]` |
| **Evidence Screenshots / Logs** | Support the findings described in this report. | `[Evidence filenames and IDs]` |

---

## 5. Findings and Evidence

### 5.1 M1 — Initial Access

**Objective:** Identify the public-facing entry points, record reconnaissance and enumeration observations, and assess initial-access behavior only to the extent supported by authorized evidence.

#### 5.1.1 Public Entry-Point and Reconnaissance Observations

| Observation | Evidence / Status |
| :--- | :--- |
| **Target homepage** | Observed at `https://medirozahospital.com`; attach homepage evidence if retained. |
| **Patient portal** | `/patient/login.php` was observed as a public navigation entry point. |
| **Staff portal** | `/staff/login.php` was observed as a public navigation entry point. |
| **HTTP response** | A browser request returned `HTTP/2 304 Not Modified`. |
| **Server header** | The observed response included `Server: LiteSpeed` and `X-Turbo-Charged-By: LiteSpeed`. |
| **Additional security headers** | Not established from the 304 response alone; verify using a suitable full response or mark as not assessed. |

The `304` response indicates that the browser's cached representation was considered unchanged. It is not, by itself, evidence of a vulnerability. The LiteSpeed response headers disclose server technology and should be treated as an informational observation unless further evidence demonstrates impact.

#### 5.1.2 Initial-Access and Enumeration Scan Evidence

The tester reports having one or more initial-access scan outputs and one or two enumeration screenshots. The exact scan findings, discovered paths, HTTP status codes, scan options, and timestamps have not been transcribed into the material supplied for drafting this report.

| Field | To be completed from original scan evidence |
| :--- | :--- |
| **Evidence ID** | `[M1-E01 / M1-E02]` |
| **Tool and version** | `[Exact tool/version]` |
| **Target and scope** | `[Exact authorized host/path]` |
| **Command / scan profile** | `[Copy exact command/options from the log]` |
| **Date and time** | `[Timestamp and timezone]` |
| **Observed result** | `[Summarise only what the screenshot/log visibly proves]` |
| **Validation status** | `[Confirmed / Not confirmed / Inconclusive]` |

#### 5.1.3 Authentication and Access-Control Evidence

The final report should include the relevant request and response pair for any authentication test, with credentials, cookies, tokens, and personal data redacted. A payload being entered or submitted does not prove an authentication bypass. A bypass finding requires evidence of an authenticated state or access to a protected test resource, together with the authorization context and a reproducible response.

| Evidence Required | Reporting Requirement |
| :--- | :--- |
| **Baseline login behavior** | Record the response for a normal invalid test account, if testing was explicitly authorized. |
| **Test input and response** | Include sanitized request/response evidence from an approved test environment. |
| **Session behavior** | Record cookie flags and session-state observations; redact cookie values. |
| **Protected-resource access** | Use synthetic accounts and test records to demonstrate access-control decisions. |
| **Conclusion** | State confirmed, not confirmed, or inconclusive. Do not claim SQL injection or bypass without direct proof. |

> **M1 Status:** Partially documented. Reconnaissance observations are recorded; detailed scan output and any claimed initial-access result must be transcribed and validated from the original evidence.

---

### 5.2 M2 — Data Extraction and Password-Hash Assessment

**Objective:** Assess the password strength of approved encrypted test PDFs through offline hash extraction and dictionary testing. The tester reports having three PDF artifacts and evidence that password hashes were cracked and password values recovered. This report deliberately does not reproduce patient identities, clinical results, raw hashes, or recovered passwords.

| Artifact | Evidence to Attach / Record | Current Status |
| :--- | :--- | :--- |
| **PDF 1** | Sanitized filename, file size/type, hash-extraction screenshot, cracking result screenshot, validation outcome. | Tester reports password recovered; verify from original log. |
| **PDF 2** | Sanitized filename, file size/type, hash-extraction screenshot, cracking result screenshot, validation outcome. | Tester reports password recovered; verify from original log. |
| **PDF 3** | Sanitized filename, file size/type, hash-extraction screenshot, cracking result screenshot, validation outcome. | Tester reports password recovered; verify from original log. |

#### 5.2.1 Assessment Procedure

1. Confirm that each PDF is an instructor-provided or explicitly authorized test artifact.
2. Record non-sensitive file metadata such as sanitized filename, file size, file type, and SHA-256 checksum.
3. Record the hash-extraction tool and version. Store extracted hashes in a restricted evidence location; do not place raw hashes in the report.
4. Record the cracking tool, version, attack mode, wordlist source, start/end time, and final status.
5. Validate recovery by opening the approved test PDF in the authorized lab. Do not copy clinical contents into the report.
6. Redact all recovered passwords. The report should state only whether the password was recovered and the general weakness (for example, weak or dictionary-based password).

#### 5.2.2 Finding M2-01 — Weak Password Protection on Test PDF Artifacts

* **Observation:** The tester reports that password-hash assessment against three PDF artifacts resulted in password recovery. This suggests that the passwords used for those test artifacts may have insufficient resistance to dictionary-based guessing.
* **Impact:** If the same password practices are used for sensitive documents, an attacker who obtains an encrypted file may be able to recover its password offline. The impact depends on whether the artifacts contain sensitive information and whether the testing was authorized.
* **Severity:** `Provisional` — to be assigned after confirming artifact sensitivity, authorization, and reproducible cracking logs.
* **Recommendation:** Use long, unique, randomly generated document passwords or authenticated portal-based document delivery. Avoid common words, predictable patterns, and password reuse. Apply access controls independently of document-level encryption.

> **M2 Status:** Tester-reported recovery for three artifacts; final validation requires the original tool logs and confirmation that the PDFs were authorized test files.

---

### 5.3 M3 — Data Exposure Assessment

**Objective:** Determine whether sensitive files, backups, or business information are unintentionally exposed through in-scope resources. No direct evidence of a database backup, staff salary register, or shareholder/capitalisation data was included in the evidence summary supplied for this draft.

| Assessment Area | Evidence Status | Report Treatment |
| :--- | :--- | :--- |
| **Directory listing / exposed paths** | Initial enumeration screenshots reportedly exist; exact paths and results not supplied. | Pending transcription and validation. |
| **Legacy database backup** | No verified backup file evidence supplied. | Not confirmed; do not claim exposure. |
| **Staff salary information** | No verified, authorized synthetic dataset evidence supplied. | Not assessed / pending approved test data. |
| **Shareholder information** | No verified, authorized synthetic dataset evidence supplied. | Not assessed / pending approved test data. |

If a potentially sensitive file is encountered on the live hospital system, do not retrieve or inspect its contents. Record the minimum necessary metadata (for example, the URL path and response status, if permitted), stop further access, and notify the instructor or authorized contact. Use synthetic backup files and synthetic HR/shareholder records for any deeper demonstration.

> **M3 Status:** Pending / not evidenced in the supplied summary. This section must be updated only if authorized, non-sensitive evidence is available.

---

### 5.4 M4 — Reporting and Retesting

M4 is completed by consolidating the verified observations from M1–M3 into this report, documenting limitations, assigning evidence-based severity, and providing remediation guidance. Retesting should be performed only within the approved scope and against the agreed acceptance criteria.

| Retest Area | Example Acceptance Criterion |
| :--- | :--- |
| **Authentication** | Invalid credentials do not create an authenticated session; errors are generic and do not disclose database details. |
| **Session management** | Session cookies use appropriate `Secure`, `HttpOnly`, and `SameSite` attributes; logout invalidates the session. |
| **Access control** | Unauthenticated users cannot access protected test resources; one test user cannot access another test user's synthetic records. |
| **Directory and backup exposure** | Sensitive directories are not browsable; backup files are outside the web root or otherwise access-restricted. |
| **Document protection** | Test documents use strong unique secrets or authenticated access; weak dictionary passwords are rejected by policy. |

---

## 6. Risk Rating Summary

| ID | Finding / Observation | Milestone | Provisional Rating | Basis / Limitation |
| :--- | :--- | :--- | :--- | :--- |
| **F-01** | LiteSpeed technology disclosure in response headers | M1 | `Informational` | Technology disclosure alone does not demonstrate exploitability. |
| **F-02** | Initial-access / enumeration observations | M1 | `Pending` | Exact scan results and validation details must be transcribed. |
| **F-03** | Password recovery reported for three PDF artifacts | M2 | `Pending` | Confirm authorized test artifacts, logs, and sensitivity before rating. |
| **F-04** | Potential directory or backup exposure | M3 | `Not confirmed` | No verified backup or sensitive-record evidence supplied. |

Risk ratings should consider likelihood, impact, exploitability, scope, and the sensitivity of affected assets. Do not assign Critical or High solely because a scan lists a path or because a password was recovered from a test artifact.

---

## 7. Recommendations and Remediation

* **Access Control:** Enforce server-side authentication and authorization checks on every protected page and file request. Verify ownership for each document request; do not rely on hidden links or client-side controls.
* **Input Handling:** Use parameterized database queries and server-side validation. Return generic authentication errors and prevent detailed SQL/database errors from reaching users.
* **Session Security:** Set `Secure`, `HttpOnly`, and appropriate `SameSite` cookie attributes. Rotate session identifiers after authentication and invalidate sessions on logout.
* **Directory and Backup Protection:** Disable directory indexing where it is not required. Keep database backups, logs, configuration files, and archives outside public web roots and restrict access.
* **Document Protection:** Use strong, unique, randomly generated passwords where document passwords are necessary. Prefer authenticated, access-controlled document delivery for sensitive reports.
* **Monitoring and Response:** Log authentication failures, access-control denials, sensitive file access, and administrative actions. Alert on unusual access patterns and retain logs according to policy.
* **Retesting:** After remediation, repeat the approved tests using synthetic accounts and test documents. Preserve before/after evidence and document the retest date and result.

---

## 8. Limitations

* This draft is based on the tester's summary of available evidence; original scan files, screenshots, and cracking logs were not embedded in the source material used to prepare this report.
* The exact initial-access technique and its successful outcome have not been independently verified in this draft.
* The three PDF artifacts and recovered password values have not been independently inspected for authorization or sensitivity. Passwords and clinical contents are intentionally omitted.
* No verified evidence of an exposed legacy database backup, staff salary register, or shareholder data was supplied for M3.
* A `304 Not Modified` response is a caching response and is not itself a vulnerability.
* Any result not supported by reproducible evidence is marked pending, not confirmed, or inconclusive.

---

## 9. Conclusion

The assessment documented public-facing entry points, server response observations, and tester-reported initial-access/enumeration and PDF password-assessment evidence. The current evidence summary supports documenting the existence of reconnaissance artifacts and reported password recovery for three PDF files, subject to authorization and log validation. M3 database-backup and confidential business-data exposure has not been established from the supplied evidence summary and remains pending.

The final submission should include the original sanitized screenshots and logs referenced in the Evidence Index, confirm the approved scope and testing dates, and ensure that all patient, credential, hash, and confidential business information is redacted. Findings should be marked confirmed only when the evidence directly supports the stated result.

---

**Prepared by:** Atharv Shinde  
**Organization:** NetworkWalks  
**Date:** 26 November 2026
