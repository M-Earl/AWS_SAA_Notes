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
* EBS Multi-Attach is limited to 16 instances
* Launch templates supercede launch configurations (more features). Launch templates are immutable and allow versions
* EC2 placement groups:
    - Cluster – packs instances close together inside an Availability Zone. Low-latency, HPC
    - Partition – spreads your instances across logical partitions. Typically used by large distributed and replicated workloads, such as Hadoop, Cassandra, and Kafka.
    - Spread – strictly places a small group of instances across distinct underlying hardware
# AWS Lambda
* Lambda ayers can be used to pull libraries/dependencies (up to 5 layers)
* Lambda can be deployed as images
# Elastic File System
* Bursting: Throughput scales with system size
* Provisioned: Throughput fixed at specified amount
# Amazon DBs
* Aurora has a reader endpoint (load balancing) and writer endpoint (changes if new db is promoted)
* Amazon Redshift Spectrum - get data from S3 without importing
* DynamoDB Accelerator (DAX) is a cache for DynamoDB
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
# CloudFront
* CloudFront is great for static data in many places
* S3 Cross Region Replication is great for dynamic data in a few places
# DataSync
* Maintains metadata
# SQS and SNS
* SQS can add filter policies on its subscribers
# VPC
* VPC endpoints are used to connect AWS --> AWS (powered by AWS PrivateLink)
* Gateway endpoints can only run S3 and DynamoDB
* NAT gateways replaced NAT instances
* Default NACL allows everything
* Clients connect to a defined port and get a response on an ephermal port
* To access an S3 bucket, Gateway Endpoint is preferred over Instance Endpoint (unless on-prem resources)
* VPC Peering - connect different VPCs together (not transitive)
* Direct Connect - establishes a dedicated connection from on-premises to AWS. Takes months to set up
* AWS Site-to-Site VPN - connect on-premises network to your Amazon VPC (AWS side: virtual private gateway, client side: customer gateway)
* AWS Global Accelerator - provides a fixed entry point to ALBs, NLBs, Elastic IPs, or EC2s (multi-region compatible)
# Disaster Recovery
* Four Types of Disaster Recovery:
    - Backup and Restore
    - Pilot Light
    - Warm Standby
    - Multi-Site
# Security
* AWS GuardDuty monitors activity found in AWS CloudTrail Events, Amazon VPC Flow Logs, and DNS Logs
