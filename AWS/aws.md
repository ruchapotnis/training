## What is an EC2 Instance?
An **EC2 (Elastic Compute Cloud) Instance** is a virtual server in the cloud that provides resizable compute capacity.

## Difference Between EC2 and Elastic Beanstalk
* **EC2 Instance:** A clean slate. You get infrastructure-as-a-service (IaaS), meaning you must manually configure the operating system, network, and install required software or libraries.
* **Elastic Beanstalk:** A platform-as-a-service (PaaS). It comes with predefined libraries, runtime environments, and automated provisioning (like load balancing and auto-scaling), allowing you to deploy apps without worrying about the underlying infrastructure.

---

## Types of EC2 Instances

### General Purpose
* Optimized for a balance of compute, memory, and networking resources.
* Best for applications requiring prompt responses, cost-effectiveness, and balanced processing (e.g., web servers, small databases).

### Compute Optimized
* Engineered for applications that require a lot of processing power from the CPU.
* Best for high-performance front-end servers, data analytics, and analyzing streaming data.

### Memory Optimized
* Designed to deliver fast performance for workloads that process large datasets in memory (RAM).
* Best for open-source databases, real-time big data analytics, and running large-scale caches.

### Storage Optimized
* Tailored for workloads that require high, sequential read and write access to very large datasets on local storage.
* Best for distributed file systems, data warehousing, and large-sized transactional databases.

### Accelerated Computing (GPU)
* Utilizes hardware accelerators (GPUs or FPGAs) to perform functions like co-processing and graphics acceleration.
* Best for heavy graphics rendering, machine learning, and 3D visualizations.

---

## EC2 Instance Pricing Models

### On-Demand
* You pay for compute capacity by the second or hour with no long-term commitments.
* The instance stays active until you choose to stop or terminate it yourself (it does not automatically delete after 1 hour).

### Dedicated Hosts / Instances
* Physical EC2 servers fully dedicated to a single organization.
* Offers high security, strict hardware isolation from other AWS vendors, and helps meet compliance or licensing requirements.

### Spot Instances
* Allows you to bid on or utilize unused AWS spare capacity at steep discounts (up to 90% off On-Demand prices).
* The instance can be reclaimed and interrupted by AWS with a 2-minute warning if they need the capacity back.

### Reserved Instances (and Savings Plans)
* Provides a significant discount (up to 72%) compared to On-Demand pricing in exchange for a commitment to a consistent amount of usage for a 1 or 3-year term.
* Allows you to plan long-term costs while still maintaining the ability to upscale or downscale capacity as needed.


## EC2 Instance Features Based on Functioning

### Burstable Performance Instances
* **Definition:** A category of General Purpose instances designed to provide a baseline level of CPU performance with the ability to burst above that baseline when needed.
* **How it works:** They accumulate "CPU credits" when running below their baseline performance. When workloads spike, they spend these credits to burst to higher capacity. If you run out of credits, performance throttles back to the baseline.
* **Use Case:** Applications where data and traffic are not constant, such as customer data analysis tools, small web servers, or development environments.

### EBS-Optimized Instances
* **Definition:** Instances designed to maximize Amazon Elastic Block Store (EBS) performance by providing dedicated throughput between the EC2 instance and the EBS volume.
* **Benefit:** Eliminates network contention between EBS I/O and other network traffic from your instance, ensuring data processes at higher and more consistent speeds.
* **Use Case:** High-throughput transactional workloads, active database management systems, or automated systems like high-frequency email auto-responders.

### Cluster Networking (Placement Groups)
* **Definition:** A configuration strategy that forms clusters of instances to meet low-latency and high-throughput networking needs.
* **How it works:** Instances are strategically placed within logical groups (like Cluster, Partition, or Spread placement groups) to optimize data transfer or ensure hardware isolation across multiple instances serving different purposes.
* **Use Case:** High-Performance Computing (HPC), tightly coupled node applications, and distributed distributed systems like search engine indexing and big data browsing.

### Dedicated Instances / Hosts
* **Definition:** Instances that run on physical hardware dedicated strictly to a single customer account or organization.
* **Benefit:** Provides complete hardware-level isolation, maximizing security, data privacy, and compliance.
* **Use Case:** Confidential data processing, government compliance workloads, and strict corporate privacy frameworks.

---

## Amazon Machine Image (AMI)
* **Definition:** An **AMI (Amazon Machine Image)** is a pre-configured template used to launch an EC2 instance.
* **What it contains:** It packages the operating system, an application server, and any necessary pre-installed software and permissions.
* **Reusability:** You can use a single AMI to launch as many identical, independent new instances as your infrastructure requires.

## AWS Lambda
**AWS Lambda** is a serverless, event-driven compute service used to automate tasks by executing code in response to specific triggers without provisioning or managing servers.

### Key Characteristics
* **Event-Driven Execution:** Functions are automatically triggered based on defined actions, such as uploading files, database updates, or HTTP requests.
* **Granular Automation:** Composes precise workflows, such as parsing an object uploaded to an S3 bucket or passing events downstream to other services.

### Event Trigger Example (S3 to Lambda Workflow)
A typical automation pattern involves linking an Amazon S3 storage bucket directly to a Lambda function to process newly added data seamlessly:
* **S3 Event Configuration:** An event notification is created within an S3 bucket's properties using the **`PUT` object option**, which tracks any new file uploads.
* **Asynchronous Execution:** When a file is uploaded, S3 fires an event notification that asynchronously invokes the targeted Lambda function.
* **Data Processing & Logging:** The triggered Lambda function extracts parameters from the event metadata—specifically the **bucket name** and the object's **file key**—to parse, decode, and print or process the uploaded file's contents (e.g., viewing structured JSON data).
* **Multi-Service Chaining:** The action can chain across other services, such as utilizing the **Amazon SNS (Simple Notification Service)** to automatically dispatch emails to designated addresses upon a successful trigger event.

---

## AWS Elastic Beanstalk
**AWS Elastic Beanstalk** is an easy-to-use Platform as a Service (PaaS) designed for deploying and scaling web applications and services developed with popular runtimes and languages.

### Core Architecture & Capabilities
* **Automated Application Deployment:** Simplifies deployment by handling the underlying infrastructure details, making applications publicly accessible immediately after a bundle upload.
* **Elastic Resource Scaling:** Automatically provisions resources up or down to dynamically match traffic fluctuations and application performance requirements.
* **Monitoring and Alerting:** Built-in health monitoring, metrics collection, and automated alerts to continuously log and manage ecosystem stability.
* **Multi-Environment Architecture:** Supports running independent copies of an application simultaneously across isolated boundaries (e.g., distinct **Development (Dev)**, **Testing (Test)**, and **Production (Prod)** environments).
* **Environment-Specific Isolation:** Structurally segments logical environments into distinct deployment pipelines, mapping unique environmental configurations and software folders for cleaner workspace management.