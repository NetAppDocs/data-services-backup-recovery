## Copilot instructions for NetApp Backup and Recovery documentation

### Repository overview
Product: NetApp Backup and Recovery

NetApp Backup and Recovery is a NetApp Console data protection service for *ONTAP* workloads, including volume, database, virtual machine, and Kubernetes application data. The service uses policy-driven protection workflows across local snapshots, secondary replication, and object storage backup targets.

### Repository structure
- `./` – Primary AsciiDoc content is stored at repository root, including overview, prerequisites, setup, workload protection, restore, API, and reference pages; filename prefixes map to content type (`concept-`, `br-start-`, `br-use-`, `prev-`, `reference-`, `task-`).
- `_include/` – Reusable include fragments for shared Kubernetes and backup/restore instructions (for example session token notes and execution hook template content).
- `_whatsnew/` – Dated release note entry files consumed by the main what’s new page.
- `redirect/` – Redirect stubs that preserve legacy URLs by mapping old permalinks to current pages.
- `media/` – Shared diagrams, screenshots, icons, and supporting visual assets used across documentation pages.

### Product-specific context
**Architecture and components:**
- *NetApp Backup and Recovery* runs through *NetApp Console* and uses a deployed *Console agent* to connect storage systems, hosts, and cloud/object targets.
- Protection spans workload-specific paths: *ONTAP volumes*, *Microsoft SQL Server*, *VMware*, *KVM*, *Hyper-V*, *Oracle Database*, and *Kubernetes*.
- Data protection patterns are built around *3-2-1* flows: source snapshots, optional secondary copies (replication), and offsite object backups.
- For Kubernetes workflows, protection and restore operations are represented through `protect.trident.netapp.io/v1` custom resources and *AppVault* references.
- Backup and restore automation is available through REST API endpoint groups such as `backup`, `restore`, `catalog`, `system`, and `job`.

**Key concepts:**
- A *workload* is the protection unit and maps by platform (for example application in Kubernetes, VM in virtualization platforms, database in database platforms).
- *Protection groups* and *policies* define scope, scheduling, retention behavior, and backup target behavior for managed resources.
- *Offsite backup targets* are discovered or added destinations such as *AWS S3*, *Azure Blob*, *Google Cloud Storage*, *StorageGRID*, and *ONTAP S3*.
- *Inventory* and *Settings* are core operational areas for discovering resources, adding credentials, integrating external managers, and controlling protection behavior.
- *SnapCenter import* is supported for Microsoft SQL Server resource onboarding, then management can be transferred to NetApp Backup and Recovery.

**Naming conventions and terminology:**
- Common UI and docs terms include *Inventory*, *Managed offsite backup targets*, *protection group*, *policy*, *backup target*, *AppVault*, and *resource transformation template*.
- Kubernetes custom resource kinds used in docs include *Snapshot*, *Backup*, *BackupRestore*, *BackupInplaceRestore*, *SnapshotRestore*, and *SnapshotInplaceRestore*.
- KVM management integration terminology uses *management platform* and references *Apache CloudStack* for host/VM discovery.
- File naming conventions indicate content role and workload scope (for example `br-use-vmware-*`, `br-use-kubernetes-*`, `br-use-mssql-*`, `prev-ontap-*`).

### Typical user workflows
**Initial service setup:** Prepare *NetApp Console* and *Console agent* → discover ONTAP/storage resources → configure credentials and settings → discover offsite backup targets → set workload-specific policies

**Workload protection and recovery:** Discover workload resources → create protection groups/policies → run scheduled or on-demand backups (snapshot/replication/object) → monitor jobs and reports → restore to same or alternate location

**Kubernetes CR-driven operations:** Discover Kubernetes clusters/apps → configure or reference *AppVault* → apply backup/snapshot CRs → validate backup artifacts and status → apply restore CRs with namespace/resource mapping as needed
