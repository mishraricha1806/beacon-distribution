# Beacon

Beacon is an early local production-readiness scanner for distributed systems.

It helps answer:

```text
Is this safe to release?
What are the top operational risks?
What should be fixed first?
What evidence is missing?
```

Beacon is currently distributed for public evaluation as a Docker image only.
There are no public native installers in this repo.

## Safe Evaluation First

For first-time evaluation, use only:

- the examples in this repo
- sanitized configuration files
- non-sensitive runtime snapshots
- local/non-production test data

Do not use:

- production credentials
- live production clusters
- secrets, tokens, private keys, or certificates
- Terraform state containing sensitive values
- customer logs, customer telemetry, or private business data

Beacon is designed to be read-only . It will not store any data .

## Try The Local UI

```bash
docker pull ghcr.io/mishraricha1806/beacon:latest

docker run --rm \
  -p 8765:8765 \
  ghcr.io/mishraricha1806/beacon:latest ui --host 0.0.0.0 --port 8765
```

Open:

```text
http://127.0.0.1:8765/
```

Use `0.0.0.0` only in the Docker command. Use `127.0.0.1` or `localhost` in
your browser.

If port `8765` is busy:

```bash
docker run --rm \
  -p 8777:8765 \
  ghcr.io/mishraricha1806/beacon:latest ui --host 0.0.0.0 --port 8765
```

Then open:

```text
http://127.0.0.1:8777/
```

## Run Example Scans

Run commands from the root of this distribution repo.

Check that examples exist:

```bash
ls examples/bad-infra
```

### Bad Infra Readiness

```bash
docker run --rm \
  -v "$PWD/examples:/workspace/examples:ro" \
  ghcr.io/mishraricha1806/beacon:latest readiness static \
  /workspace/examples/bad-infra \
  --environment prod \
  --no-html \
  --no-open-report
```

This intentionally shows unsafe production-readiness findings.

### Black Friday Readiness

```bash
docker run --rm \
  -v "$PWD/examples:/workspace/examples:ro" \
  ghcr.io/mishraricha1806/beacon:latest readiness static \
  /workspace/examples/demo-black-friday \
  --environment prod \
  --no-html \
  --no-open-report
```

### Black Friday Runtime Snapshot

```bash
docker run --rm \
  -v "$PWD/examples:/workspace/examples:ro" \
  ghcr.io/mishraricha1806/beacon:latest diagnose snapshot \
  /workspace/examples/demo-black-friday/runtime-snapshot.yaml \
  --no-html \
  --no-open-report
```

## What Beacon Checks Today

Beacon currently has support for:

- Kafka readiness checks
- Kubernetes manifest checks
- Terraform/static infrastructure checks
- runtime snapshot diagnostics
- API to Kafka to Consumer to Database flow scenarios
- grouped root-cause style findings
- production-readiness score and next actions

The product direction is:

```text
Deterministic checks first.
Clear operational reasoning.
No hidden telemetry.
No black-box magic.
```

## Feedback Wanted

Beacon is early. Feedback is welcome from:

- SREs
- DevOps engineers
- platform engineers
- Kafka engineers
- Kubernetes engineers
- backend engineers
- release/governance engineers

Useful feedback:

- missing readiness checks
- false positives
- confusing output
- safer distribution ideas
- new runtime scenarios
- examples from real production-readiness reviews, with sensitive details removed

Please open an issue using one of the templates.

## Security Notes

- Beacon should be evaluated with examples or sanitized inputs first.
- Do not provide production credentials.
- Do not provide sensitive Terraform state.
- Do not provide private keys, tokens, or certificates.
- Do not connect Beacon to production clusters during initial evaluation.
- If you find a security issue, use the security concern issue template or the
  contact path listed in `SECURITY.md`.

## Image

```text
ghcr.io/mishraricha1806/beacon:latest
```

After a tagged image is published, prefer pinning a version:

```text
ghcr.io/mishraricha1806/beacon:0.1.7
```

