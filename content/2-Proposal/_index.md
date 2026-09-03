---
title: "Proposal"
date: 2026-07-21
weight: 2
chapter: false
pre: " <b> 2. </b> "
---


# Website Upload and Document Management on AWS

## Web Application Architecture Combining Amazon EC2, Amazon S3, Amazon RDS, AWS Lambda, IAM, and VPC

### 1. Executive Summary

This proposal presents a solution for building a **Website Upload and Document Management System** on the AWS cloud platform. The system allows users to upload documents to the website, store documents on Amazon S3, manage document information using Amazon RDS, and perform operations such as viewing the document list, downloading, and deleting documents.

The application is built using a Web Application model, in which the user interface communicates with the backend through APIs. The backend is deployed on **Amazon EC2** and uses Spring Boot to handle business logic and connect to AWS services.

Document files are not stored directly on EC2 but are centrally stored on **Amazon S3**. The **Amazon RDS** database only stores document metadata such as file name, file type, file size, upload time, and the corresponding S3 Object Key.

The system is placed within **Amazon VPC**, allowing network connections between EC2 and RDS to be organized and controlled. **AWS IAM** is used to control access permissions for AWS resources, especially the permissions granted to EC2 to access S3.

In addition to the normal upload flow, **AWS Lambda** is used to process events when a new document is uploaded to S3. Lambda can perform tasks such as logging, checking metadata, or performing additional document-processing steps without requiring a dedicated server.

This architecture separates application processing, file storage, and data storage, while providing a foundation for future system scalability.

---

### 2. Problem Statement

#### Current Problems

* **Dependence on server disk capacity**: As the number of documents increases, the server's available storage capacity may become insufficient.

* **Difficulty in scaling the system**: If additional EC2 instances are required to handle high traffic, storing files directly on each server can lead to distributed data.

* **Difficulty in file management**: Storing thousands or millions of documents on the server filesystem makes organization, backup, and data management more complicated.

* **Risk of data loss when the server fails**: If files exist only on a single EC2 instance, a failure of that instance may directly affect the data.

* **Insufficient separation between data and application**: The server must both process requests and handle file storage.

* **Difficulty in implementing automated file processing**: When documents need to be processed after upload, the application must perform all processing tasks on the server.

#### Proposed Solution

The system is designed according to the core principle: **EC2 handles application processing -- S3 stores files -- RDS stores metadata -- Lambda processes events -- IAM controls permissions -- VPC controls the network**.

The architecture is divided into independent components:

1. **Web Application**: Provides an interface for users to upload and manage documents.

2. **Amazon EC2**: Runs the Spring Boot backend, receives requests from the website, and handles business logic.

3. **Amazon S3**: Stores the actual document files.

4. **Amazon RDS**: Stores metadata and document management information.

5. **AWS Lambda**: Automatically processes new files uploaded to S3.

6. **AWS IAM**: Controls access permissions between EC2, S3, and AWS services.

7. **Amazon VPC**: Provides a private network environment for organizing EC2, RDS, and related components.

This architecture clearly separates **Compute, Storage, Database, Security, and Network** responsibilities.

#### Benefits

* **Separation of storage and processing**: EC2 focuses on application processing, while S3 handles document storage.

* **Scalability**: S3 can scale with the number of documents without requiring an increase in EC2 disk capacity.

* **Enhanced security**: IAM controls access permissions, while VPC helps prevent direct Internet access to RDS.

* **Automated processing**: Lambda can be automatically triggered when a new document is uploaded to S3.

---

### 3. Solution Architecture

#### Overall Architecture Diagram

![Website upload Architecture](/images/2-Proposal/overall_architecture.png)

#### Details of the main processing flows in the architecture:

##### 1. Flow A --- Document Upload

* **A1**: The user selects a document on the website.

* **A2**: The frontend sends an upload request to the Spring Boot backend running on Amazon EC2.

* **A3**: The backend checks the file name, file type, and file size.

* **A4**: The backend uses the AWS SDK to upload the file to Amazon S3.

* **A5**: After a successful upload, the backend stores the file metadata and S3 Object Key in Amazon RDS.

* **A6**: The backend returns the upload result to the frontend.

##### 2. Flow B --- Document Download

* **B1**: The user selects the Download function on the website.

* **B2**: The frontend sends the document ID to the backend.

* **B3**: The backend searches for the corresponding metadata in RDS.

* **B4**: The backend retrieves the document's S3 Object Key.

* **B5**: The backend accesses S3 to retrieve the file and returns it to the user.

##### 3. Flow C --- Document Deletion

* **C1**: The user sends a request to delete a document.

* **C2**: The backend checks the document information in RDS.

* **C3**: The backend deletes the corresponding object from S3.

* **C4**: The backend deletes the document metadata from RDS.

* **C5**: The backend returns the result to the frontend.

##### 4. Flow D --- Event Processing with Lambda

* **D1**: A new file is uploaded to S3.

* **D2**: S3 generates an ObjectCreated Event.

* **D3**: The event triggers AWS Lambda.

* **D4**: Lambda performs document-processing tasks such as checking metadata, writing logs, or generating additional processed data.

#### AWS Services Used

- **Amazon EC2**: Runs the Spring Boot backend and provides REST APIs.

- **Amazon S3**: Stores document files.

- **Amazon RDS**: Stores metadata and document management information.

- **AWS Lambda**: Processes events when new documents are uploaded.

- **AWS IAM**: Manages access permissions for EC2 and AWS services.

- **Amazon VPC**: Builds the network environment and controls connections between components.

---

### 4. Technical Implementation

#### Implementation Phases

1. **Phase 1: Analysis & Design**

    *   Analyze upload, download, deletion, and document management functions.

    *   Design the metadata database and AWS architecture.

2. **Phase 2: Website Development**

    *   Build the frontend using HTML/CSS/JavaScript.

    *   Develop the Spring Boot backend and REST APIs.

3. **Phase 3: Amazon S3 & RDS Integration**

    *   Create the S3 Bucket and integrate the AWS SDK into Spring Boot.

    *   Create the database on Amazon RDS and store document metadata.

4. **Phase 4: EC2, IAM & VPC Deployment**

    *   Deploy Spring Boot to Amazon EC2.

    *   Configure an IAM Role for EC2 to access S3 according to the Least Privilege principle.

    *   Design the VPC, Public Subnet, Private Subnet, and Security Group.

5. **Phase 5: Lambda Integration & Testing**

    *   Configure the S3 ObjectCreated Event to trigger Lambda.

    *   Test document upload, download, deletion, and access permissions.

#### Technical & Security Requirements

- **IAM Authorization**: Apply the Least Privilege principle and grant EC2 only the S3 permissions it requires.

- **RDS Protection**: Place RDS in a Private Subnet and restrict the Security Group to allow connections only from EC2.

- **S3 Protection**: Do not make the entire bucket public and control access to objects.

- **Upload File Validation**: Check the MIME type, extension, and file size before storing the file.

- **Credential Protection**: Do not hard-code AWS Access Keys and Secret Keys in the source code; use an IAM Role for EC2.

- **Data Encryption**: Use HTTPS/TLS for data in transit and AWS encryption mechanisms for stored data when required.

---

### 5. Roadmap & Deployment Milestones

```
+-----------------------------------------------------------------------------------+
| Phase 1: Analysis & Design                                                       |
|   - Analyze upload, download, and delete functions                               |
|   - Design the database and AWS architecture                                     |
+-----------------------------------------------------------------------------------+
                                      |
                                      v
+-----------------------------------------------------------------------------------+
| Phase 2: Website Development                                                     |
|   - Build the Frontend using HTML/CSS/JavaScript                                 |
|   - Develop the Spring Boot Backend and REST API                                 |
+-----------------------------------------------------------------------------------+
                                      |
                                      v
+-----------------------------------------------------------------------------------+
| Phase 3: S3 & RDS Integration                                                     |
|   - Configure the S3 Bucket                                                       |
|   - Connect Spring Boot to RDS and store metadata                                |
+-----------------------------------------------------------------------------------+
                                      |
                                      v
+-----------------------------------------------------------------------------------+
| Phase 4: EC2, IAM & VPC                                                           |
|   - Deploy Spring Boot on EC2                                                     |
|   - Configure IAM Role, VPC, Subnet, and Security Group                          |
+-----------------------------------------------------------------------------------+
                                      |
                                      v
+-----------------------------------------------------------------------------------+
| Phase 5: Lambda & Testing                                                         |
|   - Configure the S3 Event and Lambda                                             |
|   - Test functionality, security, and error handling                             |
+-----------------------------------------------------------------------------------+
```

---

### 6. Budget Estimate

Actual costs depend on the Region, resource configuration, file storage capacity, EC2 running time, and number of requests. The estimates below are intended for a small system used for learning purposes.

| AWS Service | Estimated Configuration / Scale | Cost |
| :--- | :--- | :--- |
| **Amazon EC2** | 1 small instance running the backend | Depends on configuration and running time |
| **Amazon S3** | Several GB of documents | Depends on storage capacity and requests |
| **Amazon RDS** | Small database for metadata | Depends on instance type and running time |
| **AWS Lambda** | Low request volume, S3 event processing | Depends on the number of requests and execution time |
| **AWS IAM** | IAM User / Role / Policy | No separate charge for basic IAM functionality |
| **Amazon VPC** | 1 VPC, Subnets, and Security Groups | Basic components do not have separate charges; some network resources may incur costs |

[!TIP]
{{% notice tip %}}
To reduce costs during learning, use resources eligible for the Free Tier when the account and Region meet the requirements, and stop or delete EC2 and RDS when they are not in use.
{{% /notice %}}
---

### 7. Risk Assessment

#### Risk Matrix & Mitigation Strategy

| Potential Risk | Impact Level | Probability | Mitigation Strategy |
| :--- | :---: | :---: | :--- |
| **EC2 instance stops running** | High | Low/Medium | Store source code and configuration so the application can be redeployed quickly. |
| **Connection to RDS fails** | High | Low | Check VPC, Security Group, subnet, and database connection configuration. |
| **Document upload fails** | Medium | Medium | Check upload errors, file size limits, and retry when necessary. |
| **Invalid file** | Medium | Medium | Check MIME type, extension, and file size before upload. |
| **Unauthorized access to S3** | High | Low | Use IAM Least Privilege and do not make the entire bucket public. |
| **AWS credentials are leaked** | High | Low | Use an IAM Role instead of hard-coding Access Keys and Secret Keys. |
| **Unauthorized access to RDS** | High | Low | Place RDS in a Private Subnet and allow access only from EC2 through the Security Group. |

---

### 8. Expected Results

* **Successful implementation of the Website Upload & Document Management System**: Users can upload, view the document list, download, and delete documents through the Web interface.

* **Application deployment on AWS**: The Spring Boot backend is deployed on Amazon EC2 instead of running only on a personal computer.

* **Centralized storage on Amazon S3**: Documents are separated from the application server and stored on a dedicated Object Storage service.

* **Metadata management using Amazon RDS**: Document information is stored in a structured database.

* **Automation with AWS Lambda**: Document upload events can trigger automated processing tasks.

* **Enhanced security**: IAM, VPC, Security Groups, and access-control mechanisms help limit unnecessary access.

* **Scalability**: The architecture can be further extended with features such as authentication, document authorization, folders, search, document sharing, and PDF processing.

The project provides an integrated practical model of **AWS Cloud Architecture and Web Application Deployment** while demonstrating the relationship between **Compute (EC2), Object Storage (S3), Database (RDS), Serverless Processing (Lambda), Identity & Access Management (IAM), and Network (VPC)**.