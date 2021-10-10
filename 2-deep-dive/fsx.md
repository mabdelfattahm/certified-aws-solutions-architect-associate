# Amazon FSx

## Amazon FSx for Windows

- EFS is a shared POSIX file system for Linux, meaning it can not be used with Windows
- FSx for Windows is a fully managed Windows file system share drive
- Supports SMB protocol and Windows NTFS
- It has Active Directory integration, ACLs and user quotas
- It is built on top of SSD, it can scale up to 10s of GB/s, millions of IOPS and 100s PB of data
- It can accessed from on-premise infrastructure
- It can be configured to be Multi-AZ (high availability)
- Data is backed-up daily to S3

## Amazon FSx for Lustre

- Lustre is a type of parallel distributed file system for large-scale computing
- Lustre is derived from "Linux" and "cluster"
- FSx for Lustre is used with machine learning and **High Performance Computing (HPC)**, example: video processing, financial modelling, electronic design automation
- Scales up to 100s GB/s, millions of IOPS, sub-ms latencies
- It has seamless integration with S3
    - Can "read" S3 as a file system
    - Can write the output of the computations back to S3
- It can be used with on-premise servers

## FSx File System Deployment Options

- **Scratch File System**
    - Temporary storage
    - Data is not replicated (doesn’t persist if file server fails)
    - High burst (6x faster, 200MBps per TiB)
    - Usage: short-term processing, optimize costs
- **Persistent File System**
    - Long-term storage
    - Data is replicated within same AZ
    - Replace failed files within minutes
    - Usage: long-term processing, sensitive data

## AWS Transfer Family

- A fully-managed service for file transfers into and out of Amazon S3 or Amazon EFS using the FTP protocol
- Supported protocols
    - AWS Transfer for FTP (File Transfer Protocol (FTP))
    - AWS Transfer for FTPS (File Transfer Protocol over SSL (FTPS))
    - AWS Transfer for SFTP (Secure File Transfer Protocol (SFTP))
- Managed infrastructure, Scalable, Reliable, Highly Available (multi-AZ)
- Pay per provisioned endpoint per hour + data transfers in GB
- Store and manage users’ credentials within the service
- ntegrate with existing authentication systems (Microsoft Active Directory, LDAP, Okta, Amazon Cognito, custom)
- Usage: sharing files, public datasets, CRM, ERP, ...

## Storage Comparison

- S3: Object Storage
- Glacier: Object Archival
- EFS: Network File System for Linux instances, POSIX filesystem
- FSx for Windows: Network File System for Windows servers
- FSx for Lustre: High Performance Computing for Linux systems
- EBS volumes: Network storage for one EC2 instance at a time
- Instance Storage: Physical storage for EC2 instance (high IOPS)
- Storage Gateway
- Snowball / Snowmobile: move large data to the cloud, physical
