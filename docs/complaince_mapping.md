# 🧩 AWS Service–Compliance Mapping and Control Alignment

This document maps AWS components used in the **Secure PAN Decryption — Serverless PrivateLink Pattern (PCI Compliant)** architecture to their corresponding regulatory and security standards.  
It provides quick reference alignment across **PCI DSS 4.0**, **ISO/IEC 27001:2022**, **DORA (EU 2022/2554)**, and **FIPS 140-2** controls.

---

## 📊 Compliance Mapping Table

| AWS Service | Primary Function | PCI DSS (3.4–3.6) | ISO 27001 (A.10, A.12) | DORA (Art. 9) | FIPS 140-2 |
|--------------|------------------|-------------------|-------------------------|----------------|--------------|
| **AWS KMS** | Encryption key management and PAN decryption | 3.4–3.6: Encryption, key lifecycle | A.10.1: Cryptographic controls | Data protection & integrity | Level 2 |
| **AWS CloudHSM** | Hardware key custody (CryptoAdmin/SysAdmin) | 3.5: Key protection | A.10.1: Secure key storage | Segregation of duties | Level 3 |
| **AWS Lambda** | Stateless compute for key ops | 3.4: Data isolation | A.12.1: Controlled execution | Operational resilience | Uses FIPS endpoints |
| **API Gateway (Private)** | Private API access via PrivateLink | 3.6: Key exchange | A.10.1.2: Key exchange | Controlled communication channel | FIPS TLS endpoints |
| **AWS PrivateLink** | Private VPC-to-VPC connection | 3.4: Encrypted transmission | A.10.1.1: Encryption in transit | ICT continuity | TLS 1.2 FIPS-compliant |
| **Amazon EKS** | PAN processing (encrypted payload only) | 3.4: No plaintext stored | A.12.4: Controlled environment | Risk segmentation | KMS encryption at rest |
| **AWS IAM & STS** | Role-based, temporary auth (SigV4) | 3.6.6: Restrict key access | A.9.2: Access control | Least privilege authentication | FIPS validated |
| **Amazon CloudWatch** | Operational monitoring | 12.10.5: Security tracking | A.12.4: Logging | ICT monitoring | N/A |
| **AWS CloudTrail** | Audit & API logging | 10.2–10.3: Audit trails | A.12.4.3: Audit review | Resilience traceability | N/A |
| **Amazon S3 (Archive)** | Immutable log retention | 3.4.1: PAN protection | A.12.3.1: Backup protection | Evidence retention | AES-256 FIPS validated |
| **Azure Sentinel** | Cross-cloud SIEM analytics | 10.6: Audit correlation | A.12.7: Event correlation | Monitoring ICT risk | TLS 1.2 FIPS compliant |

---

## 🧾 Summary

Each AWS service aligns to specific compliance and security objectives:  
- **AWS KMS** enforces encryption lifecycle and cryptographic control.  
- **CloudHSM** provides hardware-level key custody for FIPS 140-2 Level 3 assurance.  
- **PrivateLink** ensures data never traverses public internet.  
- **IAM + STS** secure cross-account access using SigV4-signed temporary credentials.  
- **CloudWatch, CloudTrail, and S3** provide immutable audit visibility.  
- **Azure Sentinel** adds continuous monitoring for DORA operational resilience.  

Together, these controls establish a **defense-in-depth architecture** that meets PCI DSS, ISO 27001, and DORA readiness requirements.

---

© 2025 Mahesh Devendran  
Cloud Architect | AWS | Serverless | DR | AI Automation | Compliance  
[LinkedIn Profile](https://www.linkedin.com/in/mahesh-devendran-83a3b214/)
