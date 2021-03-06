# Overview

This charm supports deployment and scaling of the Homestead component of a Project Clearwater system.  See http://www.projectclearwater.org for more information on Project Clearwater.

# Usage

The Homestead service should be deployed as part of a Clearwater system.  A Clearwater system can be deployed in a Juju environment by creating a config.yaml file then running the following commands.

    juju deploy --config config.yaml clearwater-route53
    juju deploy --config config.yaml clearwater-ellis
    juju deploy --config config.yaml clearwater-bono
    juju deploy --config config.yaml clearwater-sprout
    juju deploy --config config.yaml clearwater-homestead
    juju deploy --config config.yaml clearwater-homer
    juju add-relation clearwater-ellis clearwater-route53:register-ellis
    juju add-relation clearwater-bono clearwater-route53:register-bono
    juju add-relation clearwater-sprout clearwater-route53:register-sprout
    juju add-relation clearwater-homestead clearwater-route53:register-homestead
    juju add-relation clearwater-homer clearwater-route53:register-homer
    juju expose clearwater-bono
    juju expose clearwater-ellis

The config.yaml configuration file takes the following format.

    clearwater-route53:
      zone: <domain>
      access_key: <ec2 access key>
      secret_key: <ec2 secret access key>
      sas: "0.0.0.0"

    clearwater-ellis:
      smtp_server: smtp.cw-ngv.com
      smtp_username: username
      smtp_password: password
      email_sender: blackhole@cw-ngv.com<mailto:blackhole@cw-ngv.com>
      signup_key: secret
      base_number: "6505550000"
      number_count: 1000
      repo: http://repo.cw-ngv.com/stable

    clearwater-bono:
      turn_workaround: password
      repo: http://repo.cw-ngv.com/stable

    clearwater-sprout:
      reg_min_expires: 400
      session_max_expires: 900
      repo: http://repo.cw-ngv.com/stable

    clearwater-homestead:
      repo: http://repo.cw-ngv.com/stable

    clearwater-homer:
      repo: http://repo.cw-ngv.com/stable

## Scale out Usage

## Known Limitations and Issues

The only currently supported DNS service for Clearwater is clearwater-route53 (when deploying in Amazon EC2), so will currently only work on EC2.  Additional DNS services will be added for other environments in future.

clearwater-homestead currently only supports running as a single unit.  Clustering support will be released shortly, which will allow units to be added to and removed from a clearwater-homestead deployment using juju add-unit and juju remove-unit commands.

Note that this charm does not current pass charm proof because its hooks use EC2 APIs directly to obtain the public IP address rather than unit-get public-address.  This is to work around what looks like a Juju bug - unit-get public-address on EC2 returns the public hostname of the unit rather than the public IP address.  Unfortunately EC2 public hostname are actually split horizon hostnames, so if you attempt to resolve the hostname from within EC2 it actually resolved to a private IP address - it will only resolve to a public address if resolved from outside EC2.

# Configuration

Clearwater has a number of configuration fields which are non-defaultable.  These are as follows.

clearwater-route53

-  `zone:` This must be set to a DNS zone name which is managed by the AWS Route53 service.
-  `access_key:` and `secret_key:` These must be set to the AWS access key and secret key of the AWS account which owns the DNS zone name.

clearwater-ellis

-  `signup_key:` This is used as a signup key on the Ellis self-provisioning portal, so should be set to a unique string for each installation.
-  `base_number:` and `number_count:` These define the telephone number range assigned to the Clearwater system.

# Contact Information

## Upstream Project Name

See http:www.projectclearwater.org and https://github.com/Metaswitch/clearwater-docs/wiki for information about clearwater.

Clearwater source code and issue list can be found at https://github.com/Metaswitch/.

The Clearwater mailing list is at lists.projectclearwater.org.
