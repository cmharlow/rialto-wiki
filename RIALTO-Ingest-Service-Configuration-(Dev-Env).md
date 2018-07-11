The dev instance of the RIALTO ingest service is running on Amazon EC2. You can get the IP address of the instance via the AWS Console.

# Service

We use Upstart to configure the service, making sure it spins up at boot time and spins down on shutdown. This start/stop configuration lives in `/etc/init/rialto-ingest-service.conf`; its PID file is in `/var/run/rialto-ingest-service.pid`; and it logs to `/var/log/rialto-ingest-service.log`.

The configuration delegates knowledge about the service and its environment variables (e.g., `GOPATH`, `RIALTO_SPARQL_ENDPOINT`, `AWS_REGION`...) to a shell script that lives at `~/bin/rialto-ingest-service.sh`. Values we care about here are: `GOPATH='/home/ec2-user/go' RIALTO_SPARQL_ENDPOINT='http://cluster-rialto-id.cluster-cthpl10nkjdp.us-east-1.neptune.amazonaws.com:8182/sparql' RIALTO_TOPIC_ARN='arn:aws:sns:us-east-1:418214828013:rialto-core' RIALTO_SNS_ENDPOINT='https://sns.us-east-1.amazonaws.com' AWS_REGION='us-east-1' AWS_PROFILE='role' PORT='8080' HOST='0.0.0.0'`.

The Go source code for the service lives in `~/go/src/github.com/sul-dlss-labs/rialto-ingest-service`.

To check on the status of the service, use `sudo status rialto-ingest-service`. Use the same command with `stop` or `start` instead of `status` to stop or start the service, respectively.

# Networking

The security group governing access to the EC2 host running this service locks down SSH and HTTP to IP address blocks within the Stanford University VPN. To access the host via SSH or HTTP, do make sure you are running the VPN in "full tunnel" mode (rather than "split-tunnel mode").



