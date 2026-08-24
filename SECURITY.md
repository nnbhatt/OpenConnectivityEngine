# Security Policy

This repository is a personal fork of [Open Integration Engine](https://github.com/OpenIntegrationEngine/engine). It does not publish an independently supported release line or make a separate security-response commitment. The upstream project controls its releases, fixes, and vulnerability-coordination process.

## Supported Versions

For supported upstream versions, use the upstream project's [security policy](https://github.com/OpenIntegrationEngine/engine/security/policy) and [GitHub Releases page](https://github.com/OpenIntegrationEngine/engine/releases). Fork-only branches and commits are development snapshots and carry no independent security-support promise.

| Source | Security support |
| --- | --- |
| Official upstream releases | As stated by the upstream project |
| This fork's branches and commits | No independent support commitment |

Do not treat a commit or successful build in this fork as an official release. Operators should prefer a current supported upstream release unless they have independently reviewed, tested, and accepted the risk of fork-specific changes.

## Reporting a Vulnerability

First reproduce the issue against the current upstream project when it is safe to do so. Report vulnerabilities present in upstream privately by following the upstream [security policy](https://github.com/OpenIntegrationEngine/engine/security/policy), currently including email to [security@openintegrationengine.org](mailto:security@openintegrationengine.org). Use a subject such as `Security report: <brief description>`.

This personal fork does not operate a separate confidential intake channel. If a vulnerability is demonstrably introduced only by fork-specific changes, do not disclose sensitive details in this repository's public issues, discussions, or pull requests. Contact the fork owner through a previously established private channel, or report the underlying issue upstream when applicable.

Do **not** open a public GitHub issue, discussion, or pull request containing vulnerability details. Do not include protected health information (PHI), personal data, production credentials, access tokens, private keys, or data copied from a live system. Use synthetic data in demonstrations and proofs of concept.

Please include, when available:

- the affected Open Integration Engine version, commit, and component;
- the deployment context needed to reproduce the behavior;
- clear reproduction steps or a minimal proof of concept using synthetic data;
- the security impact and the privileges or user interaction required;
- known mitigations or workarounds;
- whether the issue has been shared with anyone else; and
- a contact address for coordinated follow-up.

Reports to upstream may cover Open Integration Engine code, bundled dependencies, official release artifacts, or upstream-controlled infrastructure. If the issue is limited to a third-party extension or a custom channel, report it to that component's owner; also report upstream when the root cause may be in Open Integration Engine.

Allow the receiving security team time for investigation and avoid public disclosure until a fix or mutually agreed disclosure date is available. Do not publish sensitive details as a way to request status.

Security researchers must use systems and data they own or are explicitly authorized to test. Avoid privacy violations, service disruption, persistence, social engineering, and access to data beyond what is necessary to demonstrate the issue.

Public issues remain appropriate for non-sensitive hardening questions, documentation gaps, or already-public dependency advisories that do not reveal a new exploit path. Use the repository’s security-question issue template and remove all secrets, sensitive data, and production details.

## Security and Compliance Responsibility

Open Integration Engine is integration software, not a certified compliance boundary. It can support workflows involving regulated data, but the project does not represent that the software or any particular deployment is automatically compliant with HIPAA, GDPR, or another legal, regulatory, or contractual framework.

Each operator is responsible for determining applicable requirements and for designing, configuring, validating, documenting, and monitoring the complete deployment. This includes infrastructure, connected systems, custom code and channels, extensions, user administration, data flows, contracts, retention rules, incident response, and workforce practices. Obtain qualified security, privacy, and legal review where required.

## Production Hardening Checklist

The committed configuration is a development starting point, not a secure production baseline. Adapt this checklist to the deployment’s threat model and applicable requirements, and record both the decisions and evidence used to validate them.

### Releases and software supply chain

- Run the latest supported stable release on a fully patched Java runtime supported by that release (the source build uses JDK 17) and a patched host or container platform.
- Subscribe to project release and security notifications. Maintain an inventory of the engine, bundled libraries, extensions, custom scripts, and connector dependencies.
- Obtain release artifacts from an expected project source and verify available signatures, checksums, provenance, and software bill of materials (SBOM) before deployment.
- Review dependency and container scan results, assess findings in the context of reachable code, and document remediation or time-bounded exceptions.
- Treat extensions, custom libraries, channel scripts, and build or deployment automation as executable code subject to review and change control.

### Identity, access, and secrets

- Replace every default, example, or shared credential before connecting the engine to production systems. Rotate credentials after suspected exposure and on an organization-defined schedule.
- Use named accounts, least privilege, separation of duties, and strong authentication. Restrict administrator client and API access to authorized management networks or a controlled access path.
- Configure password and lockout controls in `server/conf/mirth.properties` to match organizational policy; the committed values are not production recommendations.
- Give database, file, API, and connector identities only the permissions each channel needs. Avoid using domain, database-owner, or other broadly privileged accounts.
- Store passwords, tokens, private keys, and keystore credentials through an approved secrets-management process. Restrict filesystem access to configuration, application-data, backup, and key material.

### Network and transport security

- Expose only required ports and connectors. Enforce firewall rules, network segmentation, ingress allowlists where practical, and controlled outbound access.
- Replace development or self-signed certificates with certificates issued and managed according to organizational policy. Protect private keys and test certificate renewal and revocation procedures.
- Require authenticated, encrypted transport for administrative access and data flows. Allow only protocol versions and cipher suites approved by the organization; disable unused protocols and connectors.
- Configure connection, read, and request timeouts plus defensible payload-size and rate limits at the engine, reverse proxy, or network control layer as appropriate.

### Data protection and channel design

- Inventory and classify every inbound, stored, transformed, logged, queued, and outbound data element. Minimize collection and propagation of PHI and personal data.
- Define and enforce retention and deletion rules for messages, attachments, logs, audit records, temporary files, exports, dead-letter queues, and backups.
- Encrypt sensitive data at rest using controls appropriate to the database, filesystem, volume, backup, and key-management architecture.
- Prevent credentials and sensitive message content from entering application logs, exception traces, alerts, metrics, support bundles, source control, or CI artifacts.
- Validate untrusted input and review transformations and scripts for injection, unsafe deserialization, path traversal, server-side request forgery, excessive resource use, and unintended data disclosure.
- Test each channel’s authentication, authorization, error handling, retry behavior, idempotency, and failure destinations before production use.

### Operations, monitoring, and resilience

- Run services under dedicated, non-privileged identities and apply restrictive ownership and permissions to binaries, configuration, data, logs, and backups.
- Centralize and protect relevant engine, operating-system, database, identity-provider, proxy, and network logs. Alert on administrative changes, repeated authentication failures, unexpected channel changes, and unusual data movement.
- Synchronize time, define an audit-record retention policy, limit audit access, and regularly verify that expected security events are captured.
- Back up configuration, channel definitions, required application data, databases, and keys according to a documented recovery design. Test restoration and disaster-recovery procedures.
- Establish capacity limits and monitoring for memory, CPU, disk, queues, database connections, and message growth so resource exhaustion fails safely and is detected promptly.
- Maintain incident-response, vulnerability-management, access-review, patching, and secure change-control procedures. Periodically test them.

### Privacy, regulatory, and deployment validation

- Complete a documented risk assessment and data-flow review for the actual deployment, including connected systems, subprocessors, cross-border transfers, and administrative access.
- Establish the contracts and organizational measures required for the use case, such as business associate agreements, data processing agreements, records of processing, privacy notices, or data-subject request procedures where applicable.
- Validate security and privacy controls before go-live and after material changes. Retain evidence of configuration reviews, tests, approvals, training, access reviews, and remediation decisions.
- Arrange independent security testing when warranted by risk. A successful build, automated scan, or default installation is not evidence that a deployment is secure or compliant.
