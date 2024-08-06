# Setup VOCODE

- Create EC2 Instance (t2-medium)
- Assign Elastic IP via AWS Console
- Create CloudFront Distribution for this ec2 (copy the public namespace for the ec2 from dashboard)
- Create Route53 Route pointing to the cloudfront distribution

Login via ssh:

`aws --profile nexteamlive --region us-east-2 ec2-instance-connect ssh --instance-id [instance_id_goes_here]`

- Install Docker

`sudo yum install docker`
`sudo systemctl enable docker.service`

- Clone this repo

cd vocode-core/apps/telephony-app

Change the .env file:

NEXTEAM_AGENT_WEBHOOK=https://dev.nexteam.ai/api/webhooks/vocode
BASE_URL=vocode.dev.nexteam.ai - this is the route53 domain we created, ensure there is not https:// in the beginning
All the other value should b empty.


sudo docker buildx build ./ -t vocode-telephony-app
docker-compose up -d

