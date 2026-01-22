# DNS Resolution Evidence

## Command Used
```bash
dig myitsac.id
```

## Sanitized Output

```bash
myitsac.id.    1599    IN    A    104.237.1.95
```

## What This Proves
- **Infrastructure Attribution:** The IP address (`104.237.1.95`) links the domain to Hosteros LLC, a US-based hosting provider.
- **Active Hosting:** At the time of investigation, DNS was resolving correctly, confirming the site was intentionally hosted.
- **Persistence After Takedown:** DNS records remained resolvable even after the hosting provider suspended the site, showing that network-level blocks don't automatically clear DNS.

## Notes

* Domain successfully resolved to an IPv4 address
* DNS resolution remained active after site takedown

---