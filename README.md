# terraform_ec2_instance_witheni

Terraform module to create EC2 instance with elastic network interface

## Dependencies

- SSHKEY <https://github.com/virsas/terraform_ec2_sshkey>
- ENI <https://github.com/virsas/terraform_ec2_eni>
- IAM ROLE <https://github.com/virsas/terraform_iam_role>

## Terraform example

``` terraform
##################
# EC2 Variable
##################
variable "ec2_server1" { 
  default = {
    # Name of the instance
    name = "server1"
    # Credit option for CPU usage. Valid values: standard, unlimited
    credits = "standard"
    # Instance size
    type = "t4g.small"
    # OS AMI
    image = "ami-07e30a3659a490be7"
    # Allow public IP address (true/false)
    public_ip = "false"
    # Type of block device mounted to the instance
    volume_type = "gp2"
    # Size of the block device
    volume_size = "30"
    # Enable or disable encryption
    volume_encrypt = true
    # Enable deletion of block device on instance termination
    volume_delete = true
  } 
}

##################
# EC2 Instance
##################
module "ec2_server1" {
  source          = "github.com/virsas/terraform_ec2_instance_witheni"

  instance        = var.ec2_server1

  # initial ssh key used to access this instance
  key             = module.ec2_sshkey_user1.name
  # elastic network interface 
  interface       = module.interface_server1.id
}
```
