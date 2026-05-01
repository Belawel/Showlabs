# AWS Multi-Region Infrastructure & Identity Governance Project #

Dette projekt demonstrerer etableringen af en sikker, skalerbar og højtilgængelig infrastruktur på AWS, kombineret med en detaljeret Identity and Access Management (IAM) og Active Directory bruger-topologi.
---
Arkitektur Oversigt
Infrastrukturen er bygget tværs over to AWS-regioner (eu-central-1 og eu-west-1) for at sikre redundans og disaster recovery.
---
### Key Infrastructure Components:
VPC Peering: Sikker forbindelse mellem VPC 1 (172.16.0.0/16) og VPC 2 (172.17.0.0/16).

High Availability: Web-servere er fordelt over flere Availability Zones (AZs) bag Classic Load Balancers.

Security Layers: Implementering af både Network ACLs (stateless) og Security Groups (stateful) for at kontrollere trafikken ned til subnethøjde.

Storage & Data: Brug af S3-buckets med cross-region backup-strategi (showlabs-bucket og showlabs-bucket-backup).

Content Delivery: CloudFront med Origin Access Control (OAC) for sikker servering af statisk indhold.
---
Identity & Access Management (IAM)
Projektet følger "Principle of Least Privilege" (PoLP). Jeg har defineret specifikke politikker for forskellige afdelinger:
---
Gruppe	Primære Rettigheder
IT-Group	Fuld S3 administration, IAM management og begrænset EC2 adgang.
Sales-Group	Read/Write adgang til specifikke forretningskritiske S3 buckets.
HR-Group	Read/Write adgang til HR-relevante dokumenter i S3.
Management	Overordnet view-adgang med restriktioner på kritiske ændringer (Billing/IAM).
