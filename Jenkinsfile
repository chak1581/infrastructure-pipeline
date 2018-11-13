properties([pipelineTriggers([githubPush()])])
node('linux') {
    git url: 'https://github.com/chak1581/infrastructure-pipeline.git', branch: 'master'
    stage('Test') {
        sh "env"
    }
    stage('GetInstances'){
         sh "aws ec2 describe-instances --region us-east-1"
    }
     stage('CreateInstance'){
       sh "aws ec2 run-instances --image-id ami-013be31976ca2c322 --count 1 \
	   --instance-type t2.micro \
	   --key-name mykeypair \
	   --security-group-ids sg-e7c4f8ab --subnet-id subnet-0ca72a22 \
	   --region us-east-1"
	  
    }
	stage('terminateInstance'){
	   def output = sh returnStdout: true, script: 'aws ec2 describe-instances | jq .Instances[0].InstanceId'|sed -e 's/^"//' -e 's/"$//'
	   sh "aws ec2 wait --region us-east-1 instance-running --instance-ids $output"
	   sh "aws ec2 terminate-instances --instance-ids $output"
	}
}
