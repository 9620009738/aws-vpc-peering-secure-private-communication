# Connectivity Test Report

## Environment

- Region: `ap-southeast-2`
- VPC A: `10.10.0.0/16`
- VPC B: `10.20.0.0/16`
- Bastion: `10.10.1.10`
- App-A: `10.10.2.10`
- App-B: `10.20.1.10`
- VPC peering connection: `pcx-021693724af9dada1`

## Results

### Test 1 — Bastion to App-A

Command:

```bash
ping -c 4 10.10.2.10
```

Observed result: 4 packets transmitted, 4 received, 0% packet loss.

Status: PASS.

### Test 2 — Bastion to App-B across VPC peering

Command:

```bash
ping -c 4 10.20.1.10
```

Observed result: 4 packets transmitted, 4 received, 0% packet loss.

Status: PASS.

### Test 3 — TCP port 22 on App-A

Command:

```bash
timeout 3 bash -c '</dev/tcp/10.10.2.10/22'
```

Observed result: the TCP connection check succeeded.

Status: PASS.

### Test 4 — TCP port 22 on App-B

Command:

```bash
timeout 3 bash -c '</dev/tcp/10.20.1.10/22'
```

Observed result: the TCP connection check succeeded across the peering path.

Status: PASS.

## Interpretation

The results demonstrate ICMP and TCP port reachability from the bastion to both private instances. They confirm the tested network paths, including communication to App-B in the peer VPC.

These tests do not establish successful SSH authentication to the private instances or validate an application protocol.

## Cleanup

After testing, all three EC2 instances were stopped. Review other retained AWS resources separately because stopping instances does not guarantee that all AWS charges cease.
