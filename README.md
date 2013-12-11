# NAME

ec2ssh - SSH to Amazon EC2 instances via tag name

# SYNOPSIS

ec2ssh \[OPTIONS\] instance-name \[SSH-OPTIONS\]

    Options:
      -? --help     Display this help and exits.
      -d --debug    Turn on debug logging.
         --list     Return a list of matching instances.
         --profile  Use a specific profile from your aws credential file.
         --region   The region to use, overrides config/env settings.
         --filters  A list of filters used to match properties for instances. For a complete reference to the available filter keys for this operation, see the Amazon EC2 API reference.
         --private  Force ssh to connect using the private dns name. 
    
    SSH-Options

    All ssh options are supported provided they are passed in *AFTER* the instance-name.

    Examples:

    # SSH to EC2 instance whose name is bowker-imageweb
    ec2ssh bowker-imageweb

    # SSH to ec2 instance using an identity file
    ec2ssh bowker-imageweb -i /path/to/identity-file

    # SSH to ec2 instance as a specific 'user'
    ec2ssh user@bowker-imageweb

    # List all ec2 instances associated with the default profile
    ec2ssh --list

    # List all ec2 instances that start with the tag name 'bowker'
    ec2ssh --list bowker*

    # SSH to ec2 instance named bowker-imageweb in a different region
    ec2ssh --region us-west-2 bowker-imageweb

    # SSH to ec2 instance and execute command 'whoami'
    ec2ssh bowker-imageweb whoami

    # SSH to ec2 instance that is part of a specific profile (non-default)
    ec2ssh --profile pqis bowker-imageweb

    # SSH to ec2 instance using it's private DNS name
    ec2ssh --private bowker-imageweb

# DESCRIPTION

Open an ssh connection to an EC2 instance where instance-name equals
tag:value.  The 'tag:' portion of instance-name is optional, and defaults to
'Name'.  A list of instances will be returned when using the --list parameter
or if more then one matching instance is found.

All ssh options are supported as long as they are passed in \*AFTER\* the
instance-name.

Please note, this command wraps the AWS Command Line Interface tool which must
be installed and configured (http://aws.amazon.com/cli/) prior to it's use.
Please follow these instructions to install the AWS CLI:

    # Install AWS CLI
    $ sudo pip install awscli

    # Configure AWS CLI 'default' profile
    $ aws configure

    # Additional profiles can be configured as follows
    $ aws configure --profile <profile-name>

# AUTHOR

Peter Williams

# LICENSE

This library is free software; you may redistribute it and/or modify it under
the same terms as Perl itself.
