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
		withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: '34e11b65-6b7a-4f79-a037-da9510da872c', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
		    sh "aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins"  
		}
	}
}
