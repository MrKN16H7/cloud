# Introduction

In managing and securing Amazon EC2 instances, several common misconfigurations can create serious security vulnerabilities if left unchecked. From exposing instance metadata to leaving snapshots publicly accessible or allowing unencrypted Amazon Machine Images (AMIs), these misconfigurations can inadvertently expose sensitive data or provide unauthorized access to critical resources.

---

## Summary

- **Public Snapshots Enumeration**: Techniques to identify publicly accessible EBS snapshots in AWS that may expose sensitive data.

---

## Public Snapshots Enumeration

Public EBS snapshots in AWS are a common source of data leakage, as they may expose sensitive information unintentionally. Public snapshots are accessible to anyone with the Snapshot ID, making it essential to ensure that snapshots are correctly configured and permissions are restricted.

### Information Needed for Enumeration

- **AWS Account ID**
- **AWS Region**

### Techniques for Enumerating Account IDs and Regions

#### 1. Finding Account ID

- **OSINT and Code Repositories**: Attackers can use GitHub’s advanced search to look for AWS account IDs in public codebases. Using search terms like `"aws_account_id"`, `"account_id"`, or `"arn:aws"` combined with the organization’s name can reveal AWS account IDs that are inadvertently exposed in code or configuration files.

#### 2. Identifying the AWS Regions in Use

Since snapshots are stored regionally, attackers seek to determine which regions an organization uses most frequently:

- **Network Probing and DNS Enumeration**: Attackers use tools like `nslookup` or `dig` on known domains to identify AWS regional endpoints. For example:
  - Querying known service endpoints, such as `*.compute.amazonaws.com`, can sometimes reveal regional information.
  - Running reverse DNS lookups on IPs associated with the target might also return region-specific AWS IP ranges.


### AWS CLI Command Example

To list all snapshots owned by your AWS account, use the following AWS CLI command:

```bash
aws ec2 describe-snapshots --owner-ids 123456789123 --query 'Snapshots[*].[SnapshotId,Description,OwnerId]' --output table
```
Replace 123456789123 with your actual AWS account ID.

Output
---------------------------------------------------
|               DescribeSnapshots                 |
+---------------------+---------------------------+
|  snap-0abcd1234efgh5678 | Production DB Backup   |
|  snap-0ijklmnop1234qrst | Web Server Logs        |
|  snap-0uvwxyz1234567890 | Customer Data Archive  |
---------------------------------------------------
