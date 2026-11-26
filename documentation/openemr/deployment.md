# OpenEMR Deployment

## 1. Overview

OpenEMR was deployed as the first healthcare application in the Healthcare IT Homelab.

OpenEMR is an open-source Electronic Health Record (EHR) and practice management platform.

The deployment uses Docker Compose to manage the application and database services.

## 2. Deployment Environment

| Component | Configuration |
|---|---|
| Host | healthcare-lab |
| Proxmox Container | CT 104 |
| Operating System | Debian 12 Bookworm |
| Container Runtime | Docker Engine |
| Orchestration | Docker Compose |
| Application | OpenEMR 8.5.0 |
| Database | MariaDB 12.3.3 |

## 3. Architecture

The deployment consists of two primary services:

- OpenEMR: Web application and EHR interface.
- MariaDB: Relational database backend.

Docker Compose manages both services.

```text
CT 104: healthcare-lab
└── Docker
    ├── OpenEMR
    │   └── Web Interface (Port 8080)
    └── MariaDB
        └── Internal Docker Network
```

## 4. Persistent Storage

Docker named volumes are used to retain application data.

| Volume | Purpose |
|---|---|
| databasevolume | MariaDB database storage |
| logvolume01 | Application logs |
| sitevolume | OpenEMR site data |

## 5. Deployment Configuration

Compose configuration:

`deployments/openemr/docker-compose.yml`

Credentials are stored in a local `.env` file excluded from Git.

## 6. Deployment and Validation

Deployment command:

```bash
docker compose up -d
```

Configuration validation:

```bash
docker compose config --quiet
```

Service verification:

```bash
docker compose ps
```

The OpenEMR web interface loaded successfully, and administrator login was completed.

**Deployment status: Operational — initial login verified.**

## 7. Security Considerations

- Generated credentials are stored locally and excluded from Git.
- Database service is not published to the host network.
- Synthetic patient data must be used exclusively.
- Access should remain restricted to the private lab network.
- Credentials and private configuration must never be committed to the public repository.

## 8. Future Work

- Configure simulated practice and facility information.
- Create provider and administrator accounts.
- Generate synthetic patient records.
- Explore patient encounters and clinical documentation.
- Explore scheduling and appointment workflows.
- Investigate FHIR interoperability.
- Document troubleshooting and maintenance procedures.

## 9. Disclaimer

This is a personal educational environment, not a production healthcare system or a HIPAA-compliant deployment.

All testing must use synthetic patient data.
