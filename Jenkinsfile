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
       aws ec2 run-instances --image-id ami-013be31976ca2c322 --count 1 \
	   --instance-type t2.micro \
	   --key-name mykeypair \
	   --security-group-ids sg-070e4f8ea1bc2c01f --subnet-id subnet-0ca72a22 \
	   --region us-east-1
    }
}
