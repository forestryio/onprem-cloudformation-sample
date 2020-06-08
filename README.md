### Deployment steps

- Install aws cli if not installed already 
  ```pip3 install awscli```

- Set up aws crendentials and profile
  ```aws configure```

- Create an AWS keypair (with default pofile)
  ```aws ec2 create-key-pair --key-name mukesh --output text  > ~/.ssh/$USER.pem```

- Create an AWS keypair (with named profile)
```aws ec2 create-key-pair --key-name mukesh --output text  --profile {profile_name} > ~/.ssh/$USER.pem```

- Deploy stack from the cli (with default pofile)
  ```aws cloudformation deploy --template-file ec2.yml --stack-name on-prem --parameter-overrides EC2Key=$USER```

- Deploy stack from the cli (with named pofile)
  ```aws cloudformation deploy --template-file ec2.yml --stack-name on-prem --profile {profile_name}--parameter-overrides EC2Key=$USER```

##### Bonus
- Describe cloudformation deployment events 
```aws cloudformation describe-stack-events --stack-name on-prem```

- Delete cloudformation stack
```
aws cloudformation delete-stack --stack-name on-prem
```
- Delete keypair
```
aws ec2 delete-key-pair --key-name $USER
```