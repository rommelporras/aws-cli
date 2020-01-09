# AWS CLI Docker Container
[![Docker Pulls](https://img.shields.io/docker/pulls/rommelporras/aws-cli.svg)](https://hub.docker.com/r/rommelporras/aws-cli/)
[![Docker Stars](https://img.shields.io/docker/stars/rommelporras/aws-cli.svg)](https://hub.docker.com/r/rommelporras/aws-cli/)

# AWS CLI Version

* [1.16.313 - Jan 09, 2020](https://github.com/aws/aws-cli/releases/tag/1.16.313)
* [1.16.305 - Dec 18, 2019](https://github.com/aws/aws-cli/releases/tag/1.16.305)

# Supported tags and Dockerfile links

- [`latest/1.16.313` (*1.16.313/Dockerfile*)](https://github.com/rommelporras/aws-cli/tree/master/1.16.313)
- [`1.16.305` (*1.16.305/Dockerfile*)](https://github.com/rommelporras/aws-cli/tree/master/1.16.305)

# Build

```
docker build -t rommelporras/aws-cli:latest .
```
or
```
docker build -t rommelporras/aws-cli:1.16.313 .
```
# Description

Docker container with the AWS CLI installed.

Using [Alpine linux](https://hub.docker.com/_/alpine/).  The Docker image is 50MB

An automated build of this image is on Docker Hub: https://hub.docker.com/r/rommelporras/aws-cli/

## Example Usage:

### Describe an instance:

    docker run -rm \
    --env AWS_ACCESS_KEY_ID=<<YOUR_ACCESS_KEY>> \
    --env AWS_SECRET_ACCESS_KEY=<<YOUR_SECRET_ACCESS>> \
    --env AWS_DEFAULT_REGION=us-east-1 \
    rommelporras/aws-cli \
    ec2 describe-instances --instance-ids i-90949d7a

output:

    {
        "Reservations": [
            {
                "OwnerId": "960288280607",
                "ReservationId": "r-1bb15137",
                "Groups": [],
                "RequesterId": "226008221399",
                "Instances": [
                    {
                        "Monitoring": {
                            "State": "enabled"
                        },
                        "PublicDnsName": null,
    ...
    ...
    }

## Example Usage with Docker Compose:
First: Update the environment credentials in `docker-compose.yml`

`docker-compose run aws s3 ls`

output:

    2019-10-17 13:07:17 sftp-bucket-ips
    2019-04-30 09:48:13 rommelporras-dev-bucket



### Return a list of items in s3 bucket

    docker run -rm \
    --env AWS_ACCESS_KEY_ID=<<YOUR_ACCESS_KEY>> \
    --env AWS_SECRET_ACCESS_KEY=<<YOUR_SECRET_ACCESS>> \
    rommelporras/aws-cli \
    s3 ls

output:

    2019-12-19 01:41:30 Assets
    2014-06-06 01:02:29 Layouts

### Upload content of your current directory (say it contains two files _test.txt_ and _test2.txt_) to s3 bucket

    docker run -rm \
    --env AWS_ACCESS_KEY_ID=<<YOUR_ACCESS_KEY>> \
    --env AWS_SECRET_ACCESS_KEY=<<YOUR_SECRET_ACCESS>> \
    -v $PWD:/data \
    rommelporras/aws-cli \
    s3 sync . s3://mybucketname

output:

    (dryrun) upload: test.txt to s3://mybucketname/test.txt
    (dryrun) upload: test2.txt to s3://mybucketname/test2.txt

doc: http://docs.aws.amazon.com/cli/latest/reference/s3/index.html

### Retrieve a decrypted Windows password by passing in your private key
We will map the private keys that resides on your local system to inside the container

    docker run -rm \
    -v <<LOCATION_TO_YOUR_PRIVATE_KEYy>>:/tmp/key.pem \
    --env AWS_ACCESS_KEY_ID=<<YOUR_ACCESS_KEY>> \
    --env AWS_SECRET_ACCESS_KEY=<<YOUR_SECRET_ACCESS>> \
    --env AWS_DEFAULT_REGION=us-east-1 \
    rommelporras/aws-cli \
    ec2 get-password-data --instance-id  <<YOUR_INSTANCE_ID>> --priv-launch-key /tmp/key.pem

Output:

    {
        "InstanceId": "i-90949d7a",
        "Timestamp": "2014-12-11T01:18:27.000Z",
        "PasswordData": "8pa%o?foo"
    }

doc: http://docs.aws.amazon.com/cli/latest/reference/ec2/get-password-data.html

## Getting your AWS Keys:

[http://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-set-up.html#cli-signup](http://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-set-up.html#cli-signup)

## Passing your keys into this container via environmental variables:

[http://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html#cli-environment](http://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html#cli-environment)

## Command line options for things like setting the region

[http://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html#cli-command-line](http://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html#cli-command-line)

## You can run any commands available to the AWS CLI

[http://docs.aws.amazon.com/cli/latest/index.html](http://docs.aws.amazon.com/cli/latest/index.html)