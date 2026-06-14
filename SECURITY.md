# Security Policy

Beacon is early software. Please evaluate it carefully.

## Safe Evaluation

Use only examples, sanitized configs, and non-sensitive snapshots for first-time
testing.

Do not use:

- production credentials
- live production clusters
- secrets or tokens
- private keys or certificates
- Terraform state containing sensitive values
- customer logs or private telemetry

## Reporting Security Concerns

If you find a security issue or an unsafe default, please open a GitHub issue
using the security concern template.

Do not include secrets, credentials, private infrastructure names, or customer
data in public issues.

## Runtime Behavior

Beacon is intended to be read-only. It should not:

- produce Kafka messages
- consume business messages
- update offsets
- mutate Kafka topics
- change ACLs
- mutate Kubernetes resources
- mutate cloud infrastructure

If you see behavior that contradicts this, please report it.

