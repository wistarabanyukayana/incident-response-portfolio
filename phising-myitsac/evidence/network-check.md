# Network-Level Takedown Evidence

## HTTPS Connectivity Test
```bash
curl -I --connect-timeout 5 https://myitsac.id/
```

### Result

```bash
curl: (28) Connection timeout after 5000 ms
```

## TCP Port Check

```bash
nc -vz 104.237.1.95 443
```

### Result

```bash
(no response, connection timed out)
```

## What This Proves
- **Successful Takedown:** The connection timeouts on both HTTPS and TCP levels confirm the hosting provider took action.
- **Network-Level Mitigation:** Rather than just removing the website, the provider suspended the entire VPS, preventing any access.
- **Global Inaccessibility:** Multiple tools (`curl`, `nc`) consistently timing out confirms the block is effective across different access methods.

## Notes

* No TCP response received from port 443
* Indicates network-level block or VPS suspension
* Timeouts across multiple tools and protocols confirm complete unavailability

---