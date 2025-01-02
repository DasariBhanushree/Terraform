provider "aws" {
  region     = "us-east-1"
  access_key = var.access_key
  secret_key = var.secret_key
}

resource "aws_instance" "my_first_ec2" {
  ami           = var.ami
  instance_type = var.instance_type
}

resource "aws_ec2_tag" "my_first_ec2" {
  resource_id = var.ami
  key         = "Terraform server"
  value       = "Test"
}

resource "aws_security_group" "New_SG" {
  name        = "New_SG"
  description = "New_SG from Terraform"
  vpc_id      = var.vpc_id

  }

resource "aws_vpc_security_group_egress_rule" "New_SG" {
  security_group_id = var.security_group_id

  cidr_ipv4   = "0.0.0.0/0"
  from_port   = 443
  ip_protocol = "tcp"
  to_port     = 443
}
