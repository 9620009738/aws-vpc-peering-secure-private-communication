# Security Notes

## Network Isolation

- VPC A uses CIDR `10.10.0.0/16`.
- VPC B uses CIDR `10.20.0.0/16`.
- The CIDR ranges do not overlap.
- App-A (`10.10.2.10`) and App-B (`10.20.1.10`) have no public IP addresses.
- Private communication between the VPCs uses the VPC peering connection.

## Administrative Access

The bastion host is the intended administrative entry point. SSH access to it should remain restricted to approved sources. EC2 Instance Connect was used for the recorded tests.

The project does not claim that direct SSH access from the developer's Windows computer was resolved.

## Security Groups

Security groups restrict traffic by protocol, port, and source. Review the actual inbound and outbound rules in the AWS account before reproducing this environment.

Do not open SSH to `0.0.0.0/0` merely to troubleshoot a connection.

## Credentials and Repository Safety

Never commit any of the following:

- SSH private keys, including `.pem` files
- AWS access keys, secret keys, or session tokens
- `.env` files containing secrets
- Local AWS credential files
- Passwords or other authentication material

Use temporary credentials or an appropriately configured AWS CLI profile for administrative work. Do not include credentials in screenshots, documentation, or command output.

## Cost and Cleanup

Stopping EC2 instances reduces compute usage but may leave billable EBS volumes, public IPv4 addresses, and other resources. Verify retained resources and account billing separately.
