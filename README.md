# Secure PAN Decryption — Serverless PrivateLink Pattern (PCI Compliant)

> **Author:** [Mahesh Devendran](https://www.linkedin.com/in/mahesh-devendran-83a3b214/)  
> **Role:** Cloud Architect | AWS | Serverless | DR | AI Automation | Compliance  
> **Whitepaper:** [📘 Download PDF](./whitepaper/Secure_PAN_Decryption_Serverless_PrivateLink_Whitepaper_v3.pdf)

---

## Overview
This repository contains the **whitepaper, design artifacts, and reference architecture** for a **serverless AWS model** enabling secure **PAN (Primary Account Number)** decryption.  
The design ensures **no plaintext PAN ever leaves the decryption boundary**, aligning with **PCI DSS, ISO 27001, DORA**, and **FIPS 140-2** frameworks.

The architecture integrates **AWS KMS**, **PrivateLink**, and optionally **CloudHSM**, achieving strong isolation, full auditability, and zero public exposure.

---

## Architecture Summary

### Components
| Layer | Account | Key AWS Services | Description |
|-------|----------|------------------|--------------|
| **Source (EKS)** | Application / Microservices | EKS, IAM, PrivateLink | Encrypts PAN using KMS public key and sends via PrivateLink |
| **Shared Services** | Central Key Distribution | Lambda, API Gateway (Private), KMS | Fetches and distributes RSA public key securely |
| **Security** | PAN Decryption Boundary | Lambda, KMS (Custom Key Store) | Decrypts PAN within AWS KMS scope |
| **Crypto (Optional)** | HSM Custody | CloudHSM | Provides hardware-backed key control (FIPS 140-2 L3) |
| **Observability** | Monitoring & Compliance | CloudWatch, CloudTrail, S3, Azure Sentinel | Captures immutable audit and security logs |

---
<img width="6456" height="2560" alt="Secure PAN Processor" src="https://github.com/user-attachments/assets/00e81411-6ff7-4326-8fe5-f0870c1ce951" />


[LinkedIn article](https://www.linkedin.com/posts/mahesh-devendran-83a3b214_aws-serverless-security-activity-7390124066550226945-gfTy/)

---

## Security & Compliance Highlights
- **End-to-End Encryption:** RSA-OAEP-SHA256 from client to Security Account  
- **Private Connectivity:** AWS PrivateLink + SigV4 authentication (no internet exposure)  
- **Key Custody:** AWS KMS (FIPS L2) + optional CloudHSM (FIPS L3, dual control)  
- **Zero Plaintext:** PAN never stored or logged in decrypted form  
- **Audit Visibility:** CloudTrail + S3 Object Lock + Azure Sentinel integration  
- **Compliance Mapping:** PCI DSS 3.4–3.6 | ISO 27001 A.10 | DORA Art. 9 | FIPS 140-2  

---

## Included Artifacts


## References & Compliance Standards

- [PCI DSS v4.0 — Payment Card Industry Standards](https://www.pcisecuritystandards.org/)
- [ISO/IEC 27001:2022 — Information Security Management](https://www.iso.org/standard/27001)
- [EU DORA Regulation (2022/2554)](https://eur-lex.europa.eu/eli/reg/2022/2554)
- [NIST FIPS 140-2 / 140-3 — Cryptographic Module Validation](https://csrc.nist.gov/projects/cryptographic-module-validation-program)
- [AWS KMS Cryptographic Documentation](https://docs.aws.amazon.com/kms/latest/developerguide/crypto-intro.html)
- [AWS CloudHSM FIPS 140-2 Certificate Reference](https://aws.amazon.com/cloudhsm/faqs/)
- [RSA-OAEP-SHA256 (RFC 8017)](https://datatracker.ietf.org/doc/html/rfc8017)
- [AWS Signature Version 4 Signing Process](https://docs.aws.amazon.com/general/latest/gr/signing_aws_api_requests.html)
