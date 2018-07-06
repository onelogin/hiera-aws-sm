
# hiera_aws_sm

#### Table of Contents

1. [Description](#description)
2. [Setup - The basics of getting started with hiera_aws_secrets_manager](#setup)
3. [Usage - Configuration options and additional functionality](#usage)
4. [Reference - An under-the-hood peek at what the module is doing and how](#reference)
5. [Limitations - OS compatibility, etc.](#limitations)
6. [Development - Guide for contributing to the module](#development)

## Description

Backend for Hiera 5 which allows lookups against Amazon Secrets Manager.

## Setup

Requires the `aws-sdk` gem to be installed and available to your
Puppetmaster.

```
package {'aws-sdk':
  ensure   => installed
  provider => puppetserver_gem
}
```

## Usage

The following is a reference of a Hiera hierarchy using hiera_aws_sm.

```
---

hierarchy:
  - name: "Hiera-AWS-SM lookup"
    lookup_key: hiera_aws_sm
    options:
      continue_if_not_found: false
      aws_access_key: AKIAIXOdummyWS76XWFAQ
      aws_secret_key: 5z6hK+x/stestmX/kfBZzlTBKdemowM9HdazfBBl
      prefix: "puppet"
      confine_to_keys:
        - '^aws_.*'

```

### Mandatory Option Keys

`name`: Human readable level name

`lookup_key`: Must be set to `hiera_aws_sm`

### Optional Option Keys

`continue_if_not_found`: Allow Puppet to lookup other data sources if the
key is not found in SecretsManager

`aws_access_key`: IAM access key to be used to connect to AWS. Should only
be used for Puppet masters running outside of AWS. Puppet masters running
within AWS should have their access to SecretsManager granted via IAM
roles.

`aws_secret_key`: IAM secret access key to be used to connect to AWS. 

`prefix`: Optional prefix to prepend to each lookup. For example, a prefix
of 'puppet' will cause lookup('password') will do a query for the secret
`puppet/password` against SecretsManager.

`confine_to_keys`: List of regex expressions on which to search
SecretsManager. If specified, hiera_aws_sm will only query SecretsManager
for keys matching at least one specified regex. If none match, Puppet is
allowed to lookup against other data sources. 


## Limitations

This module is only compatible with Hiera 5 (Puppet 4.9+)

## Development

Author: David Hayes [d.hayes@accenture.com]

## Release Notes

## TBD
- confine_to_keys
- access keys usage

