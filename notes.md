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
