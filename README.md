# Overview

This charm supports deployment and scaling of a Project Clearwater system.  See http://www.projectclearwater.org for more information on Project Clearwater.

# Usage

A Clearwater system can be deployed in a Juju environment by creating a config.yaml file then running the following commands.

    git clone https://github.com/Metaswitch/clearwater-juju.git
    JUJU_REPOSITORY=clearwater-juju/charms juju-deployer -c clearwater-juju/charms/bundles/clearwater/bundle.yaml -c bundle-config.yaml

An example of the bundle-config.yaml configuration file is at [bundle-config.yaml.example](bundle-config.yaml.example).

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
