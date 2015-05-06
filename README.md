# Introduction

ec2ssh is a set of tools that simplifies working with Amazon EC2 instances by
allowing you to connect to instances via their tag name.

# Usage

## ec2host

Get a list of all ec2 instances

```
$ ec2host
```

Get a list of ec2 instances with tag names starting with 'nginx'

```
$ ec2host nginx*
```

Get a list of ec2 instances in the 'us-west-2' region

```
$ ec2host --region us-west-2
```

Get a list of ec2 instances that are part of a specific profile (non-default)

```
$ ec2host --profile pqis
```

Get a list of ec2 instances with a tag name 'system' with value of 'centos'

```
$ ec2host system:centos
```

Get a list of ec2 instances that are 64 bit

```
$ ec2host --filters Name=architecture,Values=x86_64
```

## ec2ssh

SSH to ec2 instance whose name is nginx1

```
$ ec2ssh nginx1
```

SSH to ec2 instance using an identity file

```
$ ec2ssh nginx1 -i /path/to/identify-file
```

SSH to ec2 instance as a specific user

```
$ ec2ssh user@nginx1
```

SSH to ec2 instance in a different region

```
$ ec2ssh --region us-west-1 nginx1
```

SSH to ec2 instance and execute command `whoami`

```
$ ec2ssh nginx1 whoami
```

SSH to ec2 instance that is part of a specific profile (non-default)

```
$ ec2ssh --profile pqis nginx1
```

SSH to ec2 instance using it's private ip

```
$ ec2ssh --private nginx1
```

## ec2dns

Add all ec2 instances to /etc/hosts

```
$ ec2dns
```

Add the private ip address of all ec2 instances to /etc/hosts

```
$ ec2dns --private
```

Add the given prefix to the tag name of each ec2 instance in the given profile to /etc/hosts

```
$ ec2dns --profile prod --prefix 'prod.'
```

Add the availability zone as a suffix to the tag name of each ec2 instance to /etc/hosts

```
$ ec2dns --suffix_az
```

# Installation

Simply copy `ec2host`, `ec2ssh` and `ec2dns` to a folder, such as `~/bin`, that
is defined in your `PATH` environment variable.

The ec2ssh suite wrap the AWS Command Line Interface tool which must be
installed and configured (http://aws.amazon.com/cli/) prior to it's use.
Please follow these instructions to install the AWS CLI:

Install AWS CLI

```
$ sudo pip install awscli
```

Configure AWS CLI 'default' profile

```
$ aws configure
```

Additional profiles can be configured as follows

```
$ aws configure --profile <profile-name>
```

# AUTHOR

Peter Williams

# LICENSE

This library is free software; you may redistribute it and/or modify it under
the same terms as Perl itself.
