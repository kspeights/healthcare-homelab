# Infrastructure – Healthcare Lab

## 1. Overview

The Healthcare IT Homelab is hosted on a dedicated Proxmox LXC container, isolated from existing home server applications and services.

The environment hosts healthcare-related applications for learning and experimentation, including Electronic Health Records (EHR), Picture Archiving and Communication Systems (PACS), medical imaging viewers, and healthcare interoperability services.

**Deployment approach:** Proxmox LXC + Debian 12 + Docker + Docker Compose.

**Project repository:** [healthcare-homelab](https://github.com/kspeights/healthcare-homelab)

## 2. Proxmox Environment

| Property | Configuration |
|---|---|
| Proxmox Node | sp8z |
| Container ID | 104 |
| Hostname | healthcare-lab |
| Operating System | Debian 12 (Bookworm) |
| Container Type | LXC |
| Privileged | No (Unprivileged) |
| Status | Running |

## 3. Resource Allocation

| Resource | Allocation |
|---|---|
| CPU | 4 Cores |
| Memory | 6 GB |
| Swap | 2 GB |
| Root Disk | 60 GB |

These resources are allocated specifically to the healthcare environment to maintain separation from existing home server workloads.

## 4. Network Configuration

| Property | Configuration |
|---|---|
| Hostname | healthcare-lab |
| IPv4 Address | 192.168.1.X (Private LAN) |
| MAC Address | Redacted |
| Network Type | LAN |
| DHCP Reservation | Configured |

The container uses a dedicated LAN IP address to provide consistent access to hosted healthcare applications.

A router DHCP reservation provides consistent addressing for the container.

## 5. Software Environment

The following tools are available in the healthcare container.

| Component | Version | Status |
|---|---|---|
| Debian | 12 (Bookworm) | Running |
| Docker Engine | 29.10.1 | Running |
| Docker Compose | 5.8.0 | Available |
| Git | 2.39.5 | Available |

Docker is managed through systemd and is enabled to start automatically.

## 6. GitHub Integration and Version Control

The healthcare lab is connected to a public GitHub repository:

**Repository:** `kspeights/healthcare-homelab`

| Property | Configuration |
|---|---|
| Repository | healthcare-homelab |
| Branch | main |
| Remote | origin |
| Authentication | SSH |
| Local Clone | Configured |

Git is used to maintain infrastructure documentation, Docker Compose configurations, deployment instructions, and project changes.

Typical workflow:

```bash
git pull
git add .
git commit -m "Describe changes"
git push
```

SSH authentication is configured using an Ed25519 key. Private keys and credentials are kept outside the public repository.

## 7. Planned Application Stack

### Electronic Health Records

- OpenEMR – Electronic Health Record and practice management system.
- MariaDB – Database backend.

### Medical Imaging

- Orthanc – DICOM server and PACS.
- OHIF Viewer – Web-based medical imaging viewer.
- DCMTK – DICOM networking and testing utilities.

### Healthcare Interoperability

- HAPI FHIR – FHIR server and interoperability testing.
- HL7 – Healthcare messaging concepts and testing.
- REST APIs – Healthcare data exchange.

### Automation and Monitoring

- n8n – Workflow automation and integrations.
- Uptime Kuma – Service availability monitoring.

**Application deployment status:** Healthcare applications not yet deployed.

## 8. Architecture

The healthcare environment uses a dedicated Proxmox LXC container running Debian 12.

Docker Compose will manage individual application services within the container.

Planned architecture:

```text
Proxmox VE
└── CT 104: healthcare-lab
    └── Debian 12 Bookworm
        └── Docker Engine
            ├── OpenEMR
            ├── MariaDB
            ├── Orthanc
            ├── OHIF Viewer
            ├── HAPI FHIR
            ├── n8n
            └── Uptime Kuma
```

## 9. Security Considerations

- Maintain separation from existing home server services.
- Use synthetic patient data exclusively.
- Avoid exposing healthcare applications directly to the public internet.
- Use authentication and access controls.
- Protect application credentials and API tokens.
- Never commit SSH private keys or secrets to GitHub.
- Maintain backups of application configurations and databases.
- Document security configurations and changes.

This environment is for educational purposes and is not a production healthcare system or a HIPAA-compliant deployment.

## 10. Deployment Progress

| Milestone | Status |
|---|---|
| Create Proxmox LXC | Complete |
| Install Debian 12 | Complete |
| Configure CPU and memory | Complete |
| Assign LAN IP | Complete |
| Configure router reservation | Complete |
| Configure GitHub repository | Complete |
| Configure SSH remote | Complete |
| Verify Docker Engine | Complete |
| Verify Docker Compose | Complete |
| Run Docker test container | Pending |
| Deploy OpenEMR | Pending |
| Deploy MariaDB | Pending |
| Deploy Orthanc PACS | Pending |
| Deploy OHIF Viewer | Pending |
| Configure FHIR interoperability | Pending |

## 11. Future Improvements

- Implement VLAN isolation for healthcare services.
- Configure centralized logging.
- Implement automated database backups.
- Configure HTTPS and reverse proxy access.
- Integrate EHR and imaging workflows.
- Build healthcare interoperability demonstrations.
- Document troubleshooting and maintenance procedures.

---

**Project:** Healthcare IT Homelab  
**Environment:** Personal educational environment  
**Purpose:** Healthcare IT administration, EHR support, PACS administration, and interoperability learning.

All testing uses synthetic data. This environment is not intended for production healthcare use.
