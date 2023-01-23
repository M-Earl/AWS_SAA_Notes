AWS Solutions Associate

# IAM and AWS CLI
* User Groups cannot contain User Groups
* AWS Cloudshell - Run a shell on AWS, mostly to utilize the CLI (can upload and download files)
* Example Policy:
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "service-prefix:action-name",
            "Resource": "*",
            "Condition": {
                "DateGreaterThan": {"aws:CurrentTime": "2020-04-01T00:00:00Z"},
                "DateLessThan": {"aws:CurrentTime": "2020-06-30T23:59:59Z"}
            }
        }
    ]
    "Principal": XXX,
}
* IAM roles are global
# EC2 Instances
* User Data: On boot code to run (default : not on restart)
* Public IP can change on stop and start (Private IP stays the same)
* t2.micro ---> t is instance class, 2 is version, micro is size
* Ports to know:
    - 21: FTP
    - 22: SSH, SFTP
    - 80: HTTP
    - 443: HTTPS
    - 3389: RDP (Remote Desktop Protocol Windows)
* Security lists only allow traffic
* Launch templates supercede launch configurations (more features). Launch templates are immutable and allow versions
* EC2 placement groups:
    - Cluster – packs instances close together inside an Availability Zone. Low-latency, HPC
    - Partition – spreads your instances across logical partitions. Typically used by large distributed and replicated workloads, such as Hadoop, Cassandra, and Kafka.
    - Spread – strictly places a small group of instances across distinct underlying hardware
* Elastic IP - mask failure by rapidly remapping the address to another instance in your account
* Elastic Fabric Adapters (EFAs) can be attached to an EC2 for HPC (high performance computing)
# Load Balancers
* Network Load Balancer - used to handle UDPT / TCP (Layer 4) while ALB is HTTP/HTTPS (Layer 7)
* * Cross-zone load balancing - allows traffic to be distributed other than 50/50 to handle different number of instances in each AZ
# AWS Lambda
* Lambda layers can be used to pull libraries/dependencies (up to 5 layers)
* Lambda can be deployed as containers
* Run for 15 minutes max
# Elastic File System (EFS)
* Bursting: Throughput scales with system size
* Provisioned: Throughput fixed at specified amount
* Amazon FSx for Lustre - HPC POSIX interface with input and output stored on S3 
# Amazon DBs
* Aurora has a reader endpoint (load balancing) and writer endpoint (changes if new db is promoted)
* Amazon Redshift Spectrum - get data from S3 without importing
* DynamoDB Accelerator (DAX) is a cache for DynamoDB
* Enhanced monitoring is a feature of RDS
* Relational DBs are best for ACID / OLAP
* Redshift - OLAP, Aurora - OLTP
* Aurora is a relational DB (performance in under a second)
* IAM DB authentication is available for MySQL and PostgreSQL. Use a short-lived token. This method provides SSL traffic
* Multi-AZ RDS is synchronous
* Aurora has 6 copies in 3 AZs. Aurora read replicas are asynchronous
* DynamoDB supports single-digit millisecond response times at any scale
* RDS Read Replicas - asynchronous replication in seconds
# Route 53
* A - hostname to IPv4
* AAAA - hostname to IPv6
* CNAME - hostname to hostname
* NS - name servers
* CNAME vs Alias:
    - CNAME: Only for non-root domain (www.something.com)
    - Alias: For non-root and root domain (something.com) 
# S3 Storage
* S3 Buckets are regional (despite the global dropdown above)
* S3 Select --> SQL query on the data
* S3 Byte Range Fetch --> Get specific bytes of an S3 file
* Transfer acceleration - quicker upload into S3 by leveraging CloudFront edge locations
* In governance mode, users need special permissions to overwrite. In compliance mode, a specified object can’t be overwritten by any user
* Legal holds are indefinite locks that supercede retention periods
* DataSync - Migrate on-premises data to AWS
* Storage Gateway - create hybrid storage solution
* Amazon S3 server access logs provide more detail than CloudTrail
* Must wait 30 days before one can transfer to IA or One Zone IA
* Amazon S3 File Gateway - file interface that enables you to store files using NFS and SMB file protocols, and access those files via NFS/SMB/S3
# EBS Storage
* EBS: The maximum ratio of provisioned IOPS to the requested volume size (in GiB) is 50:1
* EBS: Magentic volumes offer lowest storage cost (HDD)
* RAID 0 - higher performance, RAID 1 - higher redundancy
* EBS Multi-Attach is limited to 16 instances
* Encryption by default is a regional setting. You cannot encrpyt unencrypted volumes (must create a new one)
# CloudFront
* CloudFront is great for static data in many places
* S3 Cross Region Replication is great for dynamic data in a few places
# DataSync
* Maintains metadata
# SQS and SNS
* SQS can add filter policies on its subscribers
* FIFO queues support up to 300 messages per second or 3,000 messages per second with batching
* SQS non-FIFO has almost unlimited throughput
# Kinesis Data Streams / Firehose
* Kinesis Data Firehose writes to S3, Redshift, Elasticsearch, HTTP or 3rd party apps (datadog, splunk, etc)
* Kinesis Data Streams - applications consume data streams (for example, containers or lambda) (1/MB/s/shard in, 2 MB/s/shard out unless fan-out)
* A single Kinesis Data Stream shard shard can ingest up to 1 MB of data per second (including partition keys) or 1,000 records per second for writes
# VPC
* VPC endpoints are used to connect AWS --> AWS (powered by AWS PrivateLink)
* Gateway endpoints can only run S3 and DynamoDB
* Default NACL allows everything
* Clients connect to a defined port and get a response on an ephermal port
* To access an S3 bucket, Gateway Endpoint is preferred over Instance Endpoint (unless on-prem resources)
* VPC Peering - connect different VPCs together (not transitive)
* Direct Connect - establishes a dedicated connection from on-premises to AWS. Takes months to set up
* AWS Site-to-Site VPN - connect on-premises network to your Amazon VPC (AWS side: virtual private gateway, client side: customer gateway)
* AWS Global Accelerator - provides a fixed entry point to ALBs, NLBs, Elastic IPs, or EC2s (multi-region compatible) (can use AnyCast IP)
* VPC Sharing - share subnets with other accounts
* Transit Gateway - connects VPCs and on-premises networks through a central hub. Eliminates complex peering relationships
    - Equal Cost Multipath (ECMP), which is supported for Site-to-Site VPN connections on a transit gateway, creates multiple tunnels
* AWS Flow Logs show activity on a VPC
* NAT gateways replaced NAT instances (more avaliable)
* Use an AWS NAT gateway to enable instances in a private subnet to connect to the internet (or AWS services) but prevent the internet from connecting to them
    - NAT gateways replaced NAT instances (more avaliable), although NAT instances have the same functionality above
    - Egress-Only Internet Gateway - same functionality above but for IPv6
* Amazon API Gateway - acts as "front door" and can throttle requests as needed
* Internet Gateway - used to provide internet access to your instances in the *public* subnet of your VPC
# Disaster Recovery
* Four Types of Disaster Recovery:
    - Backup and Restore
    - Pilot Light
    - Warm Standby
    - Multi-Site
# Security
* AWS GuardDuty monitors activity found in AWS CloudTrail Events, Amazon VPC Flow Logs, and DNS Logs
* Amazon Detective - uses logs and machine learning (ML) to highlight potential security issues (integrates with GuardDuty)
* AWS Shield is used to protect against DDoS
* AWS Network Firewall - protect VPCs, AWS WAF - protect HTTP, LBs, API Gateway, CloudFront
* Network Access Analyzer - VPC feature that reports on unintended access to your AWS resources
* Service control policies (SCPs) - a type of organization policy used to define maximum available permissions for all accounts in your organization
* AWS Control Tower - handles security of multiple accounts and services
* Symmetric key - same key encrypt and decrypt. Asymmetric key - public key to encrypt and private to decrypt
* Use identity federation in AWS via: AWS IAM Identity Center (successor to AWS SSO) or AWS IAM
# AWS Keys
* AWS Security Token Service (STS) - temporary credentials
* AWS Certificate Manager (ACM) handles SSL/TLS and can generate AWS Health Events
* CloudHSM (Hardware Security Module) - A more controllable KMS (can delete keys forever)
# Cloud Managers
* AWS Config - shows you resource configurations and changes
* AWS Secrets Manager - manage, retrieve, and rotate database credentials, API keys, and other secrets
    - AWS Systems Manager Parameter Store - lets you store variables (and can encrpyt with KMS)
    - AWS Systems Manager Run Command - lets you remotely and securely manage configuration
* AWS Service Catalog - used to manage catalogs of IT services from virtual machine images, servers, software, databases, and other resources
* AWS Resource Access Manager (AWS RAM) - used to share resources across accounts in an AWS organization
# AWS Machine Learning Services
* Amazon Polly - turns text into speech
* Amazon Comprehend - understands the content of text. Has a specialty for medical
* Amazon Textract - extract text from documents (optical character recognition (OCR))
* Amazon Lex - have a conversation just like Alexa (commonly used for chatbots)
* Amazon Rekognition - identify patterns in pictures/videos
* AWS Sagemaker - create and train machine learning algorithms
# Other Services
* Amazon Kendra - add search services
* AWS Connect - call center via AWS
* AWS Proton - deploy containers
* AWS Prometheus - monitoring and alerting service for containers
* AWS EMR - PB data processing, analytics and machine learning (Apache Spark, Apache Hive, Presto)
* AWS Application Migration Service (AWS MGN) is the primary migration service recommended for lift-and-shift migrations. Replaces CloudEndure and SMS
* AWS Application Discovery Service - track the migration status of your on-premises applications from the Migration Hub
* AWS Simple Workflow Service - used to aid distributed workflows (more particular than step functions)
* AWS Step Functions - write state machines in JSON
* AWS Trusted Advisor can be used to monitor service limits
* AWS Pinpoint - used to run simple campaigns
a* AWS X-Ray - APM for your AWS services 
* AWS AppSync is a serverless GraphQL and Pub/Sub API service to build applications
* NFS and SMB - File Gateway, iSCSI - Volume Gateway
* Amazon Managed Granafa - open-source analytics to query, visualize, and alert on your metrics, logs, and traces
* Users need access keys to utilize the AWS CLI
* AWS Audit Manager - simplify compliance with regulations and industry standards
* Amazon S3 Storage Lens - use for organization-wide visibility into S3 usage and activity
* CloudWatch logs agent needs to be installed on EC2 instances
* Amazon AppFlow - automate data flows between SaaS applications (for example, Salesforce) and AWS
