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
* User Data: On boot code to run
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
# Elastic File System
* Bursting: Throughput scales with system size
* Provisioned: Throughput fixed at specified amount
# RDS and Aurora and Elasticache
* Aurora has a reader endpoint (load balancing) and writer endpoint (changes if new db is promoted)
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
# Cloudfront
* Cloudfront is great for static data in many places
* S3 Cross Region Replication is great for dynamic data in a few places
# DataSync
* Maintains metadata
# SQS and SNS
* SQS can add filter policies on its subscribers
