# Phishing Site Takedown – myitsac.id

## Summary
In January 2026, a phishing website hosted at `myitsac.id` was identified. The site selectively served a fake password change form and was confirmed to use the GoPhish phishing framework. This report documents the investigation, technical analysis, response actions, and outcome.

---

## Timeline
| Date       | Action |
|-----------|--------|
| 2026-01-22 | Initial discovery of suspicious URL parameter `?rid=…` serving fake form |
| 2026-01-22 | DNS and IP resolution performed; infrastructure attribution to Hosteros LLC |
| 2026-01-22 | HTTP headers analyzed; presence of GoPhish identified |
| 2026-01-22 | Abuse report submitted to Hosteros LLC and Google Safe Browsing |
| 2026-01-22 | Network-level block confirmed via TCP and HTTP timeout checks |
| 2026-01-23 | Incident considered resolved; site inaccessible |

---

## Technical Analysis

### DNS and IP Information
```

Domain: myitsac.id
IP Address: 104.237.1.95
Registrar: PT Registrasi Neva Angkasa (PANDI)
Hosting Provider: Hosteros LLC
Nameservers: nsx1.domainesia.com, nsx2.domainesia.com

```

### HTTP Header Evidence
```

$ curl -I [https://myitsac.id/?rid=dummy](https://myitsac.id/?rid=dummy)
HTTP/1.1 200 OK
Server: nginx/1.24.0 (Ubuntu)
X-Server: gophish
Content-Type: text/html; charset=utf-8

```

> `X-Server: gophish` indicates use of GoPhish phishing framework.

### Certificate Transparency
```

Issuer: Let’s Encrypt
Common Name: myitsac.id
Valid From: 2026-01-06
Valid To: 2026-04-06

```

### Observations
- Root domain returned HTTP 404.
- Only the URL with parameter (`?rid=…`) served the phishing form.
- DNS resolved correctly, but the IP is currently unreachable.
- Network-level suspension confirmed by TCP timeout and `curl` timeout.

---

## Actions Taken
1. Verified suspicious behavior and HTTP headers.
2. Collected DNS, WHOIS, and IP attribution information.
3. Submitted abuse report to hosting provider (Hosteros LLC) via email.
4. Reported URL to Google Safe Browsing.
5. Monitored site availability using safe commands (`curl`, `nc`).
6. Avoided submitting any real credentials during investigation.

---

## Outcome / Resolution
- TCP connections to `104.237.1.95:443` timed out.
- `curl` requests to both root and parameterized URLs timed out.
- Hosting provider applied a network-level suspension (null routing).
- Site is currently inaccessible globally.

---

## Indicators of Compromise (IOCs)
```

Domain: myitsac.id
IP Address: 104.237.1.95
URL pattern: [https://myitsac.id/?rid=](https://myitsac.id/?rid=)*
Framework: GoPhish

```

---

## Evidence Files
Detailed technical evidence is documented in the `evidence/` folder:
- [DNS Resolution](./evidence/dns.md) – Shows domain-to-IP mapping and infrastructure attribution
- [HTTP Headers](./evidence/http-headers.md) – Confirms GoPhish framework identification
- [TLS Certificate](./evidence/certificate.md) – Establishes timeline and infrastructure setup
- [Network Takedown](./evidence/network-check.md) – Proves successful site suspension
- **Phishing Form Screenshot** (`evidence-form.png`) – Visual documentation of the phishing page before takedown

## Lessons Learned
- Phishing campaigns often use conditional URL parameters to avoid detection.
- GoPhish can be identified via HTTP headers (`X-Server: gophish`).
- Hosting provider abuse reporting can result in rapid network-level takedowns.
- DNS resolution may persist after takedown, but the site is unreachable.

---

## Evidence (Sanitized)
- **Command Logs:** Safe outputs of `dig`, `curl -I`, `nc -vz`.
- **Screenshots:** Only show the form layout **without any submitted credentials**.
- **Certificate screenshots:** Shows CN and validity period.
- **WHOIS output:** Remove any email addresses or personal contact info.

**Example of sanitized `curl` output:**
```

$ curl -I --connect-timeout 5 [https://myitsac.id/?rid=dummy](https://myitsac.id/?rid=dummy)
HTTP/1.1 200 OK
Server: nginx/1.24.0 (Ubuntu)
X-Server: gophish
Content-Type: text/html; charset=utf-8

```

**Example of sanitized `dig` output:**
```

; <<>> DiG 9.18.39 <<>> myitsac.id
;; ANSWER SECTION:
myitsac.id.  1599 IN A 104.237.1.95

```

> ✅ No real credentials, personal emails, or sensitive data are included.

---

## References
- [crt.sh](https://crt.sh) – Certificate Transparency logs  
- PANDI WHOIS database  
- Hosting provider: Hosteros LLC abuse contact  
- Google Safe Browsing reporting portal
```

---