# Security Policy

## Purpose & Scope

This repository (`https://github.com/Instancium/hub`) distributes public trust anchors (`/keys`), signed official documents (`/docs`), and signed driver packages (`/drivers`). It contains no executable source code; cryptographic verification logic is maintained in [Instancium/trust](https://github.com/Instancium/trust).

> [!WARNING]
> **Experimental Mode (Pre-2.0):** Until the Instancium ecosystem reaches release `2.0`, trust anchors and keys published in this repository may be rotated without backward compatibility.

### In Scope

Please report immediately if you observe any of the following:

- **Fingerprint mismatch** between `/keys/*.pub`, `README.md`, compiled `TrustConstants.g.cs`, and the DNS TXT record at `_trust.instancium.com`.
- **Suspected compromise** of the active `Release Key` or unauthorized commits/releases in this repository.
- **Signature or hash verification failures** for published files under `/docs`, `/drivers`, or GitHub Releases.
- **Accidental exposure** of any private key material (e.g., `*.key.json`).

### Out of Scope

- Vulnerabilities in the verification library or CLI itself — report those in [Instancium/trust](https://github.com/Instancium/trust/security/advisories/new).
- Vulnerabilities inside third-party upstream drivers under `/drivers` (report to upstream maintainers).

## Reporting an Incident

**Do NOT open a public GitHub issue for suspected key compromise or tampering.**

Report confidentially via:

1. **GitHub Private Vulnerability Reporting** (Preferred): [GitHub Security Advisories](https://github.com/Instancium/hub/security/advisories/new)
2. **Direct Email**: **support@instancium.com** with subject `[SECURITY] Instancium Hub - <brief description>`.

Please include the affected file path or release tag, observed vs. expected SHA-256 fingerprints, and the output of `Instancium.Trust.Cli verify` or `nslookup -type=TXT _trust.instancium.com` if applicable.

## Response Timeline

| Stage | Timeframe |
| --- | --- |
| Initial acknowledgment | 3 business days |
| Assessment & key/artifact verification | 7 business days |
| Remediation / key rotation (if confirmed) | As soon as verified; critical compromises prioritized immediately |

---

Thank you for helping protect the integrity of the Instancium trust chain.