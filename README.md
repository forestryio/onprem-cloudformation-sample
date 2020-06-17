### Deployment steps

- Install aws cli if not installed already 
  ```pip3 install awscli```

- Set up aws crendentials and profile
  ```aws configure```

- Create an AWS keypair (with default pofile)
  ```aws ec2 create-key-pair --key-name $USER --query 'KeyMaterial' --output text  > ~/.ssh/$USER.pem```

- Create an AWS keypair (with named profile)
```aws ec2 create-key-pair --key-name $USER --query 'KeyMaterial' --output text  --profile {profile_name} > ~/.ssh/$USER.pem```

- Deploy stack from the cli (with default pofile)
  ```
  MyPubIP=`curl ifconfig.me` && \
  aws cloudformation deploy --template-file ec2.yml --stack-name $USER-on-prem --parameter-overrides EC2Key=$USER MyPubIP=$MyPubIP/32
  ```

- Deploy stack from the cli (with named pofile)
  ```
  MyPubIP=`curl ifconfig.me` && \
  aws cloudformation deploy --template-file ec2.yml --stack-name $USER-on-prem --profile {profile_name} --parameter-overrides EC2Key=$USER MyPubIP=$MyPubIP/32
  ```

- Get Public IP addresses to SSH 
```
aws ec2 describe-instances --profile {profile_name} --query 'Reservations[*].Instances[*].PublicIpAddress' --output text
```

##### Bonus
- Describe cloudformation deployment events 
```aws cloudformation describe-stack-events --stack-name $USER-on-prem```

- Delete cloudformation stack
```
aws cloudformation delete-stack --stack-name $USER-on-prem
```
- Delete keypair
```
aws ec2 delete-key-pair --key-name $USER
```