# Docker on an AWS EC2 instance.

This guide will demonstrate how to prepare an AWS EC2 instance to use Docker.

## Create EC2 Instance.
	1. Logon to AWS EC2 Console
	2. Create EC2 t2.micro instance - Free tier
	3. Accept the usual settings
	4. Connect into the EC2 instance

## Install Docker on EC2.

```bash
sudo yum update -y
sudo amazon-linux-extras install docker
sudo service docker start
sudo usermod -a -G docker ec2-user

**Logout and back into EC2 to start using the docker cmd
Run: docker info
```
## Essential Docker Commands:

| Description                                         | Command       |
| -------------                                       | ------------- |
| Check the docker version                            | $docker --version  |
| Check which containters are downloaded              | $docker images  |
| To run a container                                  | $docker run |
| To stop a container                                 | $docker stop  |

## Running LogStash on an EC2 Instance:

	1. Create Dir to download LogStash tar file
	2. sudo curl -O  https://artifacts.elastic.co/downloads/logstash/logstash-7.15.0-linux-x86_64.tar.gz
	3. tar -zxvf logstash-7.15.0-linux-x86_64.tar.gz
	
	Change the memory heap size for the JVM from 1Gb to 400Mb, to stop JVM mem error:
	1. sudo vi jvm.options
	2. Change -XMS1g to -XMS400m
	3. Change -XMx1g to -XMS400m
	4. Save and close the file and run LogStash:
	5. Sudo bin/logstash -e "input {stdin {} } output {stdout{} } "


## Following Conf files added to repo:

| Conf File                                           | Description       |
| -------------                                       | ------------- |
| PipelineStandardInandOut.conf                       | Standard Input and Output from LogStash terminal  |
| PipelineStandardJsonInput.conf                      | Supports Json input for LogStash |
| PipelineStandardRubydebug.conf                      | Prints Output to terminal via key value pair  |
