# Cloud Security Controls

This document outlines the active **200 security controls** enforced across our multi-cloud infrastructure scanning engine, broken down by provider and resource type.

---

## 1. Amazon Web Services (AWS)

### 📦 Storage & File Systems
* **S3 Buckets:**
  * AWS S3 buckets **must** have server-side encryption enabled.
  * AWS S3 buckets **must not** be publicly accessible.
  * AWS S3 buckets **must** have versioning enabled for data recovery.
* **Block Storage:**
  * AWS EBS volumes **must** have encryption enabled at rest.
* **Network File Storage:**
  * AWS EFS file systems **must** have encryption enabled.

### 🗄️ Databases
* **RDS Instances:**
  * AWS RDS database instances **must** have encryption enabled.
  * AWS RDS database instances **must** have automated backup retention enabled.

### 🔐 Identity & Access Management (IAM)
* **IAM Users:**
  * All AWS IAM users **must** have Multi-Factor Authentication (MFA) enabled.

### ⎈ Container Orchestration
* **EKS Clusters:**
  * AWS EKS clusters **must** have Role-Based Access Control (RBAC) enabled.

---

## 2. Microsoft Azure

### 📦 Storage
* **Storage Accounts:**
  * Azure storage accounts **must not** be publicly accessible.
  * Azure storage accounts **must** have data encryption enabled.

### 🗄️ Databases
* **SQL Servers:**
  * Azure SQL servers **must** have automated backup retention enabled.
  * Azure SQL servers **must** retain backups for a minimum duration of **180 days**.

### ⎈ Container Orchestration
* **AKS Clusters:**
  * Azure AKS clusters **must** have Role-Based Access Control (RBAC) enabled.

---

## 3. Google Cloud Platform (GCP)

### 📦 Storage
* **Cloud Storage Buckets:**
  * GCP storage buckets **must not** be publicly accessible.
  * GCP storage buckets **must** have object versioning enabled.
  * GCP storage buckets **must** have encryption enabled.

### ⎈ Container Orchestration
* **GKE Clusters:**
  * GCP GKE clusters **must** run on a fully supported master node version.
  * GCP GKE clusters **must** have basic authentication disabled.
  * GCP GKE clusters **must** have Role-Based Access Control (RBAC) enabled.
