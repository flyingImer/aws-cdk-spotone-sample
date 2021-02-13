[![awscdk-run](https://img.shields.io/badge/Deploy%20with-AWSCDK.RUN-blue)](https://awscdk.run)
# aws-cdk-spotone-sample

A sample CDK application to create one durable spot instance with [cdk-spot-one](https://github.com/pahud/cdk-spot-one)

# sample

Refresh sso profile:

```sh
aws sso login --profile <sso-profile-name>
```

Convert sso profile to credentials profile:

```sh
AWS_PROFILE=<sso-profile-name> /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/pahud/gitpod-workspace/main/utils/refresh_credentials.sh)"
```

Create one instance with spot fleet and block duration:

```sh
npx cdk deploy --profile <credentials-profile-name> --require-approval never \
-c instance_type=t3a.xlarge \
-c spot_block_duration=2 \
-c stackName=SpotOneFleet-yet-another
```

Create single spot instance only(no fleet):

```sh
npx cdk deploy \
-c use_default_vpc=1 \
-c instance_only=1
```

Ssh to Spot EC2 instance:

```sh
./ec2-connect SpotOneFleet-yet-another ~/.ssh/some_rsa.pub <credentials-profile-name>
```