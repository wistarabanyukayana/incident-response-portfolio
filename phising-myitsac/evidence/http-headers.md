# HTTP Header Evidence

## Command Used
```bash
curl -I https://myitsac.id/?rid=dummy
```

## Sanitized Response Headers

```bash
HTTP/1.1 200 OK
Server: nginx/1.24.0 (Ubuntu)
X-Server: gophish
Content-Type: text/html; charset=utf-8
```

## What This Proves
- **Confirmed Attack Framework:** The `X-Server: gophish` header definitively identifies the use of GoPhish, a known phishing-as-a-service platform.
- **Active Phishing Infrastructure:** The 200 OK response confirms the server was actively serving content at the time of investigation.
- **Selective Content Delivery:** Combined with the 404 on root, this proves the attacker intentionally configured the site to serve phishing forms only on specific URLs.

## Notes

* `X-Server: gophish` confirms the use of the GoPhish phishing framework
* No request body or credentials were submitted

---