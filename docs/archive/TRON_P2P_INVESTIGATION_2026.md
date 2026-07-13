# Sanitized TRON P2P Investigation Archive

**Archive date:** 2026-07-13  
**Disposition:** Invalid / not reportable  
**Disclosure status:** Closed; no active report  
**Historical tracker:** HackerOne `#3676543`

## Purpose

Preserve the investigation history, invalidation analysis, cleanup actions, and requirements for any future authorized validation without retaining live infrastructure addresses, operational denial-of-service commands, or executable impact workflows.

## Original hypothesis

The investigation considered whether unauthenticated malformed traffic sent to the TRON peer service could trigger disproportionate resource consumption, disconnect churn, synchronization loss, or node availability degradation.

The repository later contained GitHub Actions workflows intended to demonstrate this hypothesis. Those workflows did not establish target-side product impact.

## Why the prior workflow was invalid

### Automatic workflow

The removed automatic workflow:

- Triggered on pushes to the default branch.
- Installed general network and load-generation utilities.
- Generated CPU load locally on the GitHub Actions runner.
- Sent generic network traffic toward public infrastructure.
- Did not construct or validate a TRON protocol message exchange.
- Did not collect victim-side node telemetry.

The local CPU load was self-inflicted runner activity and could not support a claim of resource exhaustion in a TRON node.

The network command used ICMP mode rather than a valid TRON P2P exchange. A destination-port argument did not convert that traffic into protocol-valid TRON peer traffic.

### Manual workflow

The removed manual workflow:

- Targeted loopback only.
- Did not start a TRON node on the runner.
- Generated local traffic without a listening product instance.
- Attempted to read a log path that was not produced by a configured TRON service.

It therefore demonstrated neither parser reachability nor product impact.

## Missing evidence

The prior material did not contain:

- A controlled TRON node under researcher authorization.
- A protocol-valid baseline connection.
- Proof that malformed input reached a specific parser or handler.
- Target-side CPU, memory, thread, queue, peer, or synchronization telemetry.
- A control run using equivalent benign traffic.
- A deterministic crash, stall, peer eviction, sync failure, or restart condition.
- Evidence that low-bandwidth attacker traffic caused disproportionate target impact.
- Reproduction independent of generic volumetric flooding.

## Final security determination

The repository artifacts were insufficient to establish a vulnerability.

**Classification:** Invalid / not reportable  
**Severity:** None  
**Required action:** Repository hygiene only; no further disclosure activity.

## Cleanup record

The following operational artifacts were removed from the default branch:

- Automatic live-target workflow.
- Manual traffic-generation workflow.
- Live peer target list.
- Network scan output containing public infrastructure details.
- Public reproduction commands.
- Unsupported severity and impact claims.

The repository README and security notice were replaced with sanitized disclosure guidance.

## Requirements for any future investigation

Future work must begin from a new hypothesis and use an isolated, explicitly authorized environment.

Minimum validation standard:

1. Run a pinned TRON node build in a local testnet or private lab.
2. Record the exact commit, configuration, JVM, resource limits, and peer topology.
3. Establish a protocol-valid baseline peer session.
4. Identify the exact parser, decoder, message type, or state transition under test.
5. Generate the smallest malformed input necessary to reach that code path.
6. Capture target-side logs, stack traces, process metrics, peer state, and synchronization state.
7. Compare malformed-input results against benign traffic at the same rate and size.
8. Demonstrate deterministic product-specific impact across repeated trials.
9. Separate parser or state-machine impact from generic bandwidth exhaustion.
10. Stop testing immediately if traffic leaves the isolated environment.

## Advancement criteria

Advance a future finding only when all of the following are present:

- Unauthenticated or clearly defined attacker capability.
- Deterministic vulnerable code-path reachability.
- Reproducible target-side security impact.
- A minimal, non-volumetric trigger where possible.
- A clear affected-version range.
- Evidence that the behavior is not expected protocol handling.
- Safe reproduction steps suitable for private disclosure.

Otherwise, park the lane as unsupported.

## Safety constraints

Do not add any of the following to this public repository:

- Live node addresses.
- Public-infrastructure target lists.
- Flooding or exhaustion commands.
- Workflows that transmit attack traffic.
- Webhook or exfiltration endpoints.
- Unverified severity claims.
- Private program correspondence or attachments.

Store sensitive raw evidence only in the private research workspace associated with the authorized engagement.
