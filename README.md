# ManageIQ
# PHPIPAM
# miq-phpipam



# PHPIPAM Module for ManageIQ

## Information
This is tested against PHPIPAM 1.2 and ManageIQ Darga using self-service provisioning on VMware




## Prereqs

In PHPIPAM take the following steps:

1. Create a user and password

2. Enable API (Administration>phpIPAM settings>Feature Settings>API)

3. Create an API key (Administration>API) for either SSL or none (crypt does not work with this extension)

Install the httparty ruby gem on the manageIQ server

```
gem install httparty
```

## Setup

After importing the extension:

Edit the default values in the schema for PHPIPAM class

- url should be set to the URL to access your phpipam API. If you access your phpipam install att https://server your url will be https://server/aip/ Include the trailing slash
- user should be set to the user created in phpIPAM
- password should be set to the password for the user created in phpIPAM
- context is the App id in phpIPAM API key
- domain should be your hosts DNS domain. This is used  to set the domain name in provisioning

## Requirements

- The description of your Subnet in phpIPAM must match  the vlan value in manageIQ provisioning variable (see below)
- Do not have duplicate Subnet description in ManageIQ

The logic this follows is:
- Get all sections in phpIPAM
- Get all subnets of all sections in phpIPAM
- Loop through each subnet to find one that matches the $evm.root['miq_provision']['vlan'] variable
- Get first address in this subnet
- Reserve this address with the hostname and return it to the provisioning process

## Information

I tagged logging info in the automation.log with IPAM so it is easy to find when troubleshooting
