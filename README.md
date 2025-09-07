# 🏰 Project Citadel: A Zero-Trust, Hybrid-Cloud Security Architecture on AWS

[![AWS Security Specialty](https://img.shields.io/badge/AWS-Security%20Specialty-FF9900?logo=amazonaws)](https://aws.amazon.com/certification/certified-security-specialty/)
[![Infrastructure as Code](https://img.shields.io/badge/IaC-Terraform-844FBA?logo=terraform)](https://www.terraform.io/)
[![Zero Trust](https://img.shields.io/badge/Security-Zero%20Trust-blueviolet)](https://www.zscaler.com/resources/what-is-zero-trust)

## 📜 Overview

**Project Citadel** is a hands-on implementation of an advanced, enterprise-grade security architecture designed to bridge a legacy on-premises data center with the AWS cloud. This project moves beyond standard application deployments to tackle complex challenges in hybrid networking, advanced identity management, data protection, and automated threat response.

The primary objective is to demonstrate mastery of the concepts required for the **AWS Certified Security - Specialty** certification by building a secure, resilient, and compliant environment from the ground up.

---

## 🚀 The Scenario

A global financial institution needs to modernize a critical, on-premises trade settlement system without performing a full migration. **Project Citadel** is the new cloud platform that will enrich on-prem data with real-time market analysis.

The core challenge is to allow cloud-native services to securely query and process highly sensitive data that must, for regulatory reasons, remain on-premises. This requires a **zero-trust** security posture where no entity, either on-prem or in the cloud, is trusted by default.

---

## 🛡️ Core Security Domains Addressed

*   **Hybrid Cloud Security:** Securely connecting and segmenting an on-premises network with AWS.
*   **Zero-Trust Networking:** Architecting a network where all traffic must be inspected and explicitly allowed, regardless of its origin.
*   **Data Protection (In-Transit, At-Rest, In-Use):** Implementing multiple layers of cryptographic controls, including protecting data during processing.
*   **Advanced Identity & Access Management:** Moving beyond standard roles to attribute-based, policy-as-code access control.
*   **Secure CI/CD & DevSecOps:** Eliminating static credentials from the deployment pipeline and integrating security into the development lifecycle.
*   **Proactive Governance & Automated Forensics:** Preventing misconfigurations before they happen and building an automated workflow to respond to incidents in real-time.

---

## 🏛️ Architectural Diagram

*(You would embed the diagram image here in your actual repository)*

![Project Citadel Architecture Diagram](https://storage.googleapis.com/gemini-prod-us-west1-0000/images/611a8779-195c-4f11-ae93-fd43c46e3e55.png)

---

## 🛠️ Key AWS Services Utilized

| Category                  | Services                                                                                                                              |
| ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| **Networking & Transit**  | AWS Transit Gateway, Site-to-Site VPN, VPC, Subnets, Route Tables, Route 53 Resolver                                                  |
| **Inspection & Protection** | **AWS Network Firewall**, AWS WAF, AWS Shield, Security Groups, NACLs                                                                 |
| **Identity & Access**     | IAM Identity Center (Successor to AWS SSO), IAM Roles, IAM Policies, **Attribute-Based Access Control (ABAC)**, **OIDC Identity Provider** |
| **Compute & Containers**  | Amazon EKS (Elastic Kubernetes Service), **AWS Nitro Enclaves**, EC2, AWS App Mesh                                                      |
| **Cryptography & Data**   | **AWS KMS (with Custom Key Store)**, **AWS CloudHSM**, Amazon S3, AWS Secrets Manager                                                   |
| **Governance & Audit**    | **AWS Config (with Conformance Packs)**, AWS CloudTrail, Amazon GuardDuty, AWS Security Hub                                             |
| **Automation & Response** | **AWS Step Functions**, AWS Lambda, AWS Systems Manager (SSM) Run Command, Amazon EventBridge                                         |

---

## ⚙️ Implementation Phases

This project is broken down into three distinct, challenging phases:

### Phase 1: The Secure Hybrid Network Foundation (Zero Trust Transit)
This phase focuses on building an immutable and highly controlled network bridge. All traffic between the on-premises data center and the Application VPC is forced through an **Inspection VPC** containing **AWS Network Firewall**. This ensures every packet is inspected against stateful rule groups, providing IDS/IPS and deep packet inspection before it can reach any application resources.

### Phase 2: Advanced Identity and Data Protection
Here, the focus shifts to the application workload. Access is governed by a sophisticated **Attribute-Based Access Control (ABAC)** model federated with an external IdP. The CI/CD pipeline is secured using **OIDC**, eliminating static IAM keys. Within the EKS cluster, **AWS App Mesh** enforces mTLS for all service-to-service communication. Most critically, highly sensitive computations are performed within **AWS Nitro Enclaves**, isolating data even from the underlying EC2 host. Finally, data at rest is protected by keys generated and stored in a dedicated **AWS CloudHSM cluster** via a KMS Custom Key Store.

### Phase 3: Proactive Governance and Automated Forensics
The final phase implements a mature security operations posture. Governance is enforced as code using a custom **AWS Config Conformance Pack** that fails deployments if resources are non-compliant. A critical **GuardDuty** finding automatically triggers a sophisticated **AWS Step Functions** workflow that orchestrates the entire incident response process: snapshotting disks, acquiring a memory dump, isolating the host, and sharing forensic artifacts with a dedicated security account.

---

## ✨ Key Security Principles Demonstrated

*   **Defense in Depth:** Multiple, overlapping layers of security controls (Network Firewall, NACL, Security Group, App Mesh, IAM).
*   **Least Privilege Access:** Granular IAM roles and ABAC policies ensure entities have only the permissions required to function.
*   **Zero Trust Architecture:** No implicit trust is granted to any entity. All connections are authenticated, authorized, and inspected.
*   **Security as Code:** The entire infrastructure, including firewall rules and IAM policies, is defined as code for repeatability and auditability.
*   **Automation:** Security is not a manual process. Threat detection, incident response, and governance are fully automated.
*   **Separation of Duties:** Use of multiple accounts (e.g., Application, Forensics) and fine-grained roles to enforce separation.