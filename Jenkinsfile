properties([pipelineTriggers([githubPush()])])

node('linux') {   
	stage('Unit Test') {    
		git 'https://github.com/xion4447/java-project.git'
		sh 'ant -f test.xml -v'
		junit 'reports/result.xml'
	}   
	stage('Build') {    
		sh 'ant -f build.xml -v'   
	}   
	stage('Deploy') {    
		sh "aws s3 cp dist/rectangle-${env.BUILD_NUMBER}.jar s3://xion4447/"   
	}
	stage('Report') {    
		sh "aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins"   
	}
}
