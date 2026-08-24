# Open Integration Engine

[![Website](https://img.shields.io/badge/website-openintegrationengine.org-blue)](https://openintegrationengine.org)
[![Discord](https://img.shields.io/discord/943670759891554316?label=Join%20our%20Discord&logo=discord&style=flat)](https://discord.gg/azdehW2Zrx)
[![Docker](https://img.shields.io/badge/docker-openintegrationengine-blue?logo=docker&style=flat)](https://hub.docker.com/u/openintegrationengine)
[![LinkedIn](https://img.shields.io/badge/linkedin-follow-blue?logo=linkedin&style=flat)](https://www.linkedin.com/company/open-integration-engine)

---
## Table of Contents

- [Mission Statement](#mission-statement)
- [Overview](#overview)
- [Why Open Integration Engine?](#why-open-integration-engine)
- [Core Features](#core-features)
- [Who It’s For](#who-its-for)
- [Building from Source](#building-from-source)
- [Security, Privacy, and Compliance](#security-privacy-and-compliance)
- [Project Values](#project-values)
- [Community and Governance](#community-and-governance)
- [History and Roadmap](#history-and-roadmap)
- [Licensing](#licensing)
- [Acknowledgments](#acknowledgments)

---
## Mission Statement

To empower seamless healthcare interoperability through an open, community-driven integration engine that is accessible, extensible, and standards-based.

---

## Overview

The **Open Integration Engine Project** is an open-source initiative committed to advancing healthcare interoperability. Building upon the foundation of **Mirth Connect**, a widely adopted integration engine, this project aims to provide healthcare organizations with a robust, flexible, and cost-effective solution for connecting disparate systems and facilitating efficient data exchange.

---

## Why Open Integration Engine?

- **Open Source Advantage**  
  Transparency, innovation, and collaborative development within the healthcare IT community.

- **Healthcare-Focused**  
  Designed to address the unique challenges of healthcare data integration, supporting standards such as HL7, FHIR, and DICOM.

- **Extensible and Customizable**  
  Modular architecture for customization and expansion to meet evolving needs.

---

## Core Features

- **Data Transformation and Mapping**  
  Convert between HL7, JSON, XML, and other formats to ensure cross-system compatibility.

- **Message Routing and Filtering**  
  Route messages using flexible, rules-based logic to streamline workflows.

- **Custom Scripting and Connectors**  
  JavaScript-based scripting and support for protocols like HTTP/S, FTP, and database connectivity.

- **Real-Time Monitoring and Alerts**  
  Visual tools for tracking message flow, performance metrics, and setting up alerts.

---

## Who It’s For

- **Integration Engineers** – Looking for a flexible, open platform for managing interfaces  
- **Health IT Teams** – Connecting EHRs, LIS, RIS, and other healthcare systems  
- **EHR Vendors** – Enhancing interoperability within their products  
- **Researchers** – Requiring reliable, standards-based integration tools

---

## Building from Source

The build is driven by Gradle through the committed wrapper; the only prerequisite is JDK 17 (see [.sdkmanrc](.sdkmanrc)):

```bash
./gradlew build              # full build + tests; distribution lands in server/setup
./gradlew clean build dist   # release form, plus extension zips in server/dist
```

On Windows use `gradlew.bat`. See [CONTRIBUTING.md](CONTRIBUTING.md) for the full command reference, the dependency policy, and how to run the server for development.

---

## Security, Privacy, and Compliance

Open Integration Engine provides capabilities that can support healthcare data integration in a security- and privacy-conscious deployment. Installing or using the software does **not** by itself make an organization or a deployment compliant with HIPAA, GDPR, or any other law, regulation, or contractual framework. Compliance depends on the complete technical and operational environment, including configuration, identity and access management, infrastructure, data handling, monitoring, policies, agreements, and risk management.

Before using Open Integration Engine with sensitive or regulated data, read the [Security Policy](SECURITY.md), follow its [production hardening checklist](SECURITY.md#production-hardening-checklist), and validate the resulting deployment against your organization’s security, privacy, legal, and regulatory requirements.

Report suspected vulnerabilities privately as described in [SECURITY.md](SECURITY.md#reporting-a-vulnerability). Do not disclose vulnerability details or sensitive data in a public issue.

---

## Project Values

- **Community-Driven Development** – Innovation through global collaboration  
- **Vendor Neutrality** – Free from proprietary constraints  
- **Security and Deployment Responsibility** – Security-conscious development, transparent reporting, and practical guidance for operators handling sensitive data

---

## Community and Governance

Engage with the community and project through:

- 🌐 **Website**: [openintegrationengine.org](https://openintegrationengine.org)  
- 💬 **Discord**: [Join our server](https://discord.gg/azdehW2Zrx)  
- 📂 **GitHub Repo**: [github.com/OpenIntegrationEngine/engine](https://github.com/OpenIntegrationEngine/engine)  
- 📥 **Releases**: [Latest Releases](https://github.com/OpenIntegrationEngine/engine/releases)  
- 🗳️ **Governance**: [Governance Docs](https://github.com/OpenIntegrationEngine/governance)  
- 🐳 **Docker Hub**: [OpenIntegrationEngine on Docker Hub](https://hub.docker.com/u/openintegrationengine)
- 🔗 **LinkedIn**: [Follow us on LinkedIn](https://www.linkedin.com/company/open-integration-engine)

Governance is structured to be transparent and inclusive, with decisions made collectively to reflect the community’s best interests.

---

## History and Roadmap

Forked from **Mirth Connect** following its shift to a proprietary model, this project continues the legacy of open healthcare integration.

### Roadmap

**Short-Term Goals**
- Stabilize codebase  
- Improve documentation  
- Expand community involvement

**Long-Term Vision**
- Support new healthcare standards  
- Enhance UX/UI  
- Grow plugin ecosystem

---

## Licensing

Licensed under the **Mozilla Public License 2.0** (MPL 2.0). See [LICENSE](./LICENSE) for details.

---

## Acknowledgments

Special thanks to the original **Mirth Connect** team and the broader open-source healthcare integration community.
