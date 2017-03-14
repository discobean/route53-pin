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

