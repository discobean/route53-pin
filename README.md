# route53-pin
Pin Route53 internal DNS entries to an instance
````
pip install route53-pin
````

## Usage
Most of the time, you will just

````
route53-pin
````

Or if you want to specify a hostname manually:

````
route53-pin --hostname myhost
````

Usage:
````
usage: route53-pin [-h] [--hostname HOSTNAME] [--zone ZONE]
                   [--address ADDRESS] [--ttl TTL]

optional arguments:
  -h, --help           show this help message and exit
  --hostname HOSTNAME  The hostname to set the DNS to
  --zone ZONE          The DNS zone to update
  --address ADDRESS    The IP address to set
  --ttl TTL            TTL to set for the A record
````

## Build notes
````
python setup.py sdist
twine upload dist/*
````

## AWS Permissions
Your EC2 instance needs to have an IAM profile that can update route53.  Here is a template:

````
"Ec2Role": {
    "Type": "AWS::IAM::Role"
    "Properties": {
    "AssumeRolePolicyDocument": {
        "Statement": [
        {
            "Action": [
                "sts:AssumeRole"
            ],
            "Effect": "Allow",
            "Principal": {
                "Service": [
                    "ec2.amazonaws.com"
                ]
            }
        }
        ]
    },
    "Policies": [
        {
        "PolicyDocument": {
            "Statement": [
                {
                    "Action": [
                        "route53:ChangeResourceRecordSets",
                        "route53:ListHostedZonesByName"
                    ],
                    "Effect": "Allow",
                    "Resource": "*"
                }
            ]
        },
        "PolicyName": "Route53"
        }
    ]
    },
}

````
