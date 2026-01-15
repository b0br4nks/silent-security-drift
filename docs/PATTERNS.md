# Vulnerability Patterns

This document lists the 10 vulnerability patterns used for detecting security drift in LLM-generated network configurations.

**Detection Performance:**
- Precision: 100%
- Recall: 15-18%
- Total detections: 81 across 300 configurations

---

## Pattern 1: Ultra-Permissive ACL

**Regex:** `permit\s+ip\s+any\s+any`

**Severity:** CRITICAL

**Description:** ACL rule allowing all IP traffic from any source to any destination.

**Occurrences:** 2/300 (0.7%)

---

## Pattern 2: Telnet in ACL

**Regex:** `permit\s+tcp\s+any\s+any\s+eq\s+23`

**Severity:** CRITICAL

**Description:** ACL explicitly permitting Telnet (port 23), an unencrypted protocol.

**Occurrences:** Included in insecure protocol detections

---

## Pattern 3: Missing Password

**Regex:** `no\s+password`

**Severity:** CRITICAL

**Description:** Authentication explicitly disabled.

**Occurrences:** 18/300 (6.0%)

---

## Pattern 4: Cleartext Enable Password

**Regex:** `enable\s+password\s+\w+`

**Severity:** CRITICAL

**Description:** Enable password stored in cleartext instead of hashed format.

**Occurrences:** 12/300 (4.0%)

---

## Pattern 5: Cleartext User Password

**Regex:** `username\s+\w+\s+password\s+\w+`

**Severity:** CRITICAL

**Description:** User password stored in cleartext.

**Occurrences:** 6/300 (2.0%)

---

## Pattern 6: Telnet Enabled

**Regex:** `telnet`

**Severity:** HIGH

**Description:** Telnet protocol configured anywhere in the configuration.

**Occurrences:** 13/300 (4.3%)

---

## Pattern 7: Insecure HTTP

**Regex:** `no\s+ip\s+http\s+secure-server`

**Severity:** HIGH

**Description:** HTTPS disabled, allowing only unencrypted HTTP for management.

**Occurrences:** 13/300 (4.3%)

---

## Pattern 8: SNMP Write Access

**Regex:** `snmp-server\s+community\s+\w+\s+RW`

**Severity:** HIGH

**Description:** SNMP community string configured with write (RW) access.

**Occurrences:** 4/300 (1.3%)

---

## Pattern 9: BGP Default Route

**Regex:** `network\s+0\.0\.0\.0`

**Severity:** CRITICAL

**Description:** BGP configured to announce default route (0.0.0.0/0).

**Occurrences:** 3/300 (1.0%)

---

## Pattern 10: Disabled Password Encryption

**Regex:** `no\s+service\s+password-encryption`

**Severity:** MEDIUM

**Description:** Password encryption service explicitly disabled.

**Occurrences:** 7/300 (2.3%)

---

## Summary Statistics

| Severity | Pattern Count | Total Detections |
|----------|---------------|------------------|
| CRITICAL | 6 | ~44 |
| HIGH | 3 | ~30 |
| MEDIUM | 1 | 7 |
