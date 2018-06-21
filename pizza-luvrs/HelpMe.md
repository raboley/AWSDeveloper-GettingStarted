# AWS and Node.js on a Mac


### Installing node software to EC2
```
curl —location https://rpm.nodesource.com/setup_6.x | sudo bash -
sudo yum install -y nodejs
```

### Testing load balancer and auto-scaling with apache benchmark
```
Ab -n 100 -c 5 http://pizza-loader-1127177182.us-west-2.elb.amazonaws.com/
```

### Moving asset files to S3 Bucket using CLI one at a time
```
aws s3 cp ./assets/js s3://pizza-luvers-russell-boley/js/ --recursive --exclude ".DS_Store"
```

```
aws s3 cp ./assets/css s3://pizza-luvers-russell-boley/css/ --recursive --exclude ".DS_Store"
```

```
aws s3 cp ./assets/pizzas s3://pizza-luvers-russell-boley/pizzas/ --recursive --exclude ".DS_Store"
```

# Getting Website code from Local computer to EC2 image

### Removing Modules folder from project to make transfer of code quicker
Usually I will have tested the code before pushing it, so want to get rid of this folder before deploying it.
```
rm -r node_modules
```

### Transfer Website code to ec2 instance (done in local terminal not in ssh)
```
scp -r -i ~/Downloads/pizza-keys.pem ./pizza-luvrs ec2-user@52.33.29.126:/home/ec2-user/pizza-luvrs
```

### SSH into the EC2

```
ssh -i ~/Downloads/pizza-keys.pem ec2-user@52.33.29.126
```

### Install modules for website

```
cd pizza-luvrs
npm install
```

### Bash script to start the web server on launch.  Paste this in the text area of the Pizza Launcher for the EC2
```
#!/bin/bash
echo "starting pizza-luvrs"
cd /home/ec2-user/pizza-luvrs
npm start
```