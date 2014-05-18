# Overview

This charm supports deployment of the BIND DNS agent for installing Project Clearwater.  See http://www.projectclearwater.org for more information on Project Clearwater.

# Usage

The Clearwater BIND service should be deployed as part of a Clearwater system.  A Clearwater system can be deployed in a Juju environment by creating a config.yaml file then running the following commands.

    juju deploy --config config.yaml clearwater-bind
    juju deploy --config config.yaml clearwater-ellis
    juju deploy --config config.yaml clearwater-bono
    juju deploy --config config.yaml clearwater-sprout
    juju deploy --config config.yaml clearwater-homestead
    juju deploy --config config.yaml clearwater-homer
    juju add-relation clearwater-ellis clearwater-bind:register-ellis
    juju add-relation clearwater-bono clearwater-bind:register-bono
    juju add-relation clearwater-sprout clearwater-bind:register-sprout
    juju add-relation clearwater-homestead clearwater-bind:register-homestead
    juju add-relation clearwater-homer clearwater-bind:register-homer
    juju expose clearwater-bind
    juju expose clearwater-bono
    juju expose clearwater-ellis

The config.yaml configuration file takes the following format.

    clearwater-bind:
      zone: <domain>

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

clearwater-bind does not currently support scaling out.

# Configuration

Clearwater has a number of configuration fields which are non-defaultable.  These are as follows.

clearwater-ellis

-  `signup_key:` This is used as a signup key on the Ellis self-provisioning portal, so should be set to a unique string for each installation.
-  `base_number:` and `number_count:` These define the telephone number range assigned to the Clearwater system.

# Contact Information

## Upstream Project Name

See http:www.projectclearwater.org and https://github.com/Metaswitch/clearwater-docs/wiki for information about clearwater.

Clearwater source code and issue list can be found at https://github.com/Metaswitch/.

The Clearwater mailing list is at lists.projectclearwater.org.
