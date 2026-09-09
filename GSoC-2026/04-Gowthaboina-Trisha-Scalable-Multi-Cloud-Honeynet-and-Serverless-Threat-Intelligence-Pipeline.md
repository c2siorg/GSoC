# Project Name# Scalable Multi-Cloud Honeynet and Serverless Threat Intelligence Pipeline
**Contributor:** Trisha Gowthaboina   **GitHub:** [TrishaG189](https://github.com/TrishaG189)   **Email:** trishagowthaboina@gmail.com   **Organization:** C2SI   **Mentor:** Charitha Elvitigala, DWath   **GSoC:** 2026 · ~360h track

# Project Abstract

Deploying honeypots across multiple cloud providers traditionally requires manual configuration, decentralized log management, and fragmented threat tracking. This project delivers an automated, scalable Infrastructure as Code (IaC) framework to deploy distributed Cowrie SSH honeypots across Amazon Web Services (AWS) and Google Cloud Platform (GCP). It utilizes Terraform for modular infrastructure provisioning with remote state locking, integrates Fluent Bit for centralized, real-time log streaming to an AWS S3 data lake, and features a serverless Python enrichment engine that contextualizes attacker IPs using IP-API and AbuseIPDB. The framework provides a fully unified threat intelligence pipeline complete with back-end log deduplication, automated VM bootstrapping, continuous integration, and a static HTML observability dashboard.

## [GSoC Project Page](https://summerofcode.withgoogle.com/programs/2026/projects/4S0sfkKW)
## [GSoC Project Proposal](https://drive.google.com/file/d/1z2NtrVT93ByNvBivxgFYG22R8Xo685Ut/view?usp=sharing)
## [GitHub Organization Repo](https://github.com/c2siorg/honeynet)
## [GitHub Personal Repo](https://github.com/TrishaG189/honeynet-framework)
## [Commits during GSoC 2026](https://github.com/TrishaG189/honeynet-framework/commits)
## [Project Wiki](https://github.com/TrishaG189/honeynet-framework/blob/main/README.md)
## [GSoC Blog](https://github.com/TrishaG189/honeynet-framework/blob/main/docs/gsoc-progress.md)

#Work Summary

**Pre-GSoC**

| **Description** | **PR** | **Merged** |
| --- | --- | --- |
| Added GitHub Actions CI pipeline for Terraform, Ansible, and shell linting | [#8](https://github.com/c2siorg/honeynet/pull/8) | ✅ |
| Provisioned remote state backend with S3 and DynamoDB locking | [#13](https://github.com/c2siorg/honeynet/pull/13) | ✅ |
| Added GCP honeypot module with VPC, strict firewall rules, and least-privilege service account | [#14](https://github.com/c2siorg/honeynet/pull/14) | ✅ |
| Documented system architecture, threat model, and data pipeline | [#15](https://github.com/c2siorg/honeynet/pull/15) | ✅ |
| Built centralized threat intelligence data pipeline using S3, Lambda, and Athena | [#35](https://github.com/c2siorg/honeynet/pull/35) | ✅ |

**GSoC Coding Period**

| **Description** | **Location / Path** | **Status** |
| --- | --- | --- |
| AWS Multi-Region Infrastructure: Modular Terraform provisioning for US, EU, India, UK | `v3/` | ✅ |
| GCP Infrastructure: Custom VPC, isolated subnets, strict firewalls, and least-privilege SA | `v4/` | ✅ |
| Remote State Backends: AWS S3/DynamoDB locking and GCP GCS locking | `v3/backend.tf`, `v4/backend.tf` | ✅ |
| Cross-Cloud Deployment Automation: Bash wrapper scripts for orchestration | Root `deploy.sh`, `destroy.sh` | ✅ |
| Automated Bootstrapping: EC2 `user_data` and GCP `metadata_startup_script` | `v3/modules/compute/`, `v4/modules/compute/` | ✅ |
| Centralized Logging: Fluent Bit systemd configuration streaming to S3 | `v3/modules/compute/main.tf` | ✅ |
| Threat Intelligence: Serverless enrichment engine querying IP-API & AbuseIPDB | `enrichment/enrich_logs.py` | ✅ |
| S3 Archive Pattern: Log deduplication and lifecycle management logic | `enrichment/enrich_logs.py` | ✅ |
| Observability: Static HTML threat dashboard generator | `enrichment/generate_dashboard.py` | ✅ |
| CI/CD & Docs: GitHub Actions pipeline, MIT License, and comprehensive README | `.github/workflows/` | ✅ |

# What Covered

## Multi-Cloud Infrastructure Automation
I completely overhauled the project's infrastructure provisioning, evolving it from a monolithic, single-region script into a highly modular Infrastructure as Code (IaC) framework utilizing Terraform. For AWS (`v3/`), I built reusable `network` and `compute` modules and utilized aliased providers (`v3/providers.tf`) to enable simultaneous, multi-region deployments across US East (N. Virginia), Europe (Frankfurt), Asia Pacific (Mumbai), and the UK (London). For Google Cloud Platform (`v4/`), I implemented a parallel architecture that provisions a custom `google_compute_network`, isolated subnets, and strict `google_compute_firewall` rules that expose only the required bait ports (22, 2222) to the internet. To shield users from Terraform complexity, I wrote dynamic `deploy.sh` and `destroy.sh` bash wrappers that parse command-line arguments to orchestrate infrastructure across different providers seamlessly.

## Automated Instance Bootstrapping & IAM
Deploying a honeypot manually introduces inconsistencies and delays. I solved this by injecting automated initialization logic directly into the cloud hypervisor using AWS `user_data` and GCP `metadata_startup_script`. When a `t3.micro` or `e2-micro` instance boots, the script automatically updates the OS, installs the Docker runtime, provisions local log directories, and launches the Cowrie SSH honeypot container with port 2222 mapped to the host. Furthermore, I enforced strict security boundaries using cloud-native Identity and Access Management (IAM). For AWS, I provisioned an `aws_iam_instance_profile` granting the exact `s3:PutObject` permissions needed for log shipping. For GCP, I created a dedicated least-privilege service account and securely injected cross-cloud AWS credentials directly into a systemd `override.conf` file, ensuring the instance metadata service cannot be exploited.

## Remote State Management
As the project scaled, relying on local `terraform.tfstate` files became a critical vulnerability that risked silent state corruption during concurrent developer operations. I architected and implemented robust remote backends for both cloud environments. The AWS deployment now utilizes a centralized, AES-256 encrypted S3 bucket (`honeynet-gsoc-26-state`) with public access fully blocked, paired with a DynamoDB table (`honeynet-state-lock`) configured for `PAY_PER_REQUEST` to handle strict concurrency locking. The GCP deployment mirrors this enterprise-grade reliability by utilizing a Google Cloud Storage (GCS) remote backend. This guarantees that multiple CI/CD pipelines or contributors can safely run deployments without encountering race conditions or overwriting infrastructure states.

## Centralized Telemetry & Enrichment Pipeline
Because honeypots are designed to be compromised and are frequently destroyed, storing logs locally is an anti-pattern. I engineered a zero-latency telemetry pipeline by configuring Fluent Bit as a systemd daemon directly within the instance bootstrapping scripts. Fluent Bit continuously tails the structured `/var/log/cowrie/cowrie.json` file and streams uncompressed payloads to a heavily restricted AWS S3 data lake (`honeynet-central-logs-2026`). 

Raw IP addresses, however, provide limited threat context. To resolve this, I developed a Python-based serverless enrichment engine (`enrich_logs.py`). Utilizing `boto3`, the engine parses the raw JSON logs from S3, extracts unique attacking IPs, and queries external intelligence feeds (IP-API for geolocation, ISP, and ASN data; AbuseIPDB for historical abuse confidence scores). To optimize execution time and prevent API rate-limiting or redundant processing, I implemented a programmatic log archival pattern that uses `s3_client.copy_object` to migrate processed files into a dedicated `archive/` partition before deleting the originals.

## Observability & CI/CD Validation
Collecting enriched data is only valuable if it is actionable. I wrote a standalone reporting module (`generate_dashboard.py`) that aggregates the enriched JSON payloads from S3 and programmatically renders a static, scannable HTML dashboard (`threat_dashboard.html`). This provides security researchers with an immediate, offline geographic and ISP breakdown of the attack telemetry. Finally, to ensure the long-term stability of the codebase, I implemented a GitHub Actions continuous integration pipeline (`terraform-validate.yml`). Triggered on every push and pull request, this pipeline provisions an Ubuntu runner to enforce `terraform fmt` across all modules and executes Python syntax compilation checks (`py_compile`), acting as a mandatory quality gate before any infrastructure drift can be merged into `main`.

# What left
- **Slack/Discord Webhook Integration:** The enrichment pipeline currently stores threat data in S3 and generates a local HTML dashboard. A logical, lightweight next step is adding a simple webhook function to `enrich_logs.py` to automatically ping a security Slack channel or Discord server whenever an IP with a critical AbuseIPDB score (e.g., >90) is detected.
