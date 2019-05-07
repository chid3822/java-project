properties([pipelineTriggers([githubPush()])]) 
node('linux'){
    stage('Unit Tests'){
      git 'https://github.com/chid3822/java-project.git'
      sh "ant -f build.xml -v"  
    }
    
    stage('Test'){
      sh "ant -f test.xml -v"
    }  
    
    stage('Deploy'){
        sh 'aws s3 cp dist/rectangle-${BUILD_NUMBER}.jar s3://chid3822-assignment-4/'
    }
     
    stage('Reports'){
withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: '1a42ea39-cfe4-4c18-b01c-f049bb4dd21e', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
    sh 'aws cloudformation describe-stack-resources --stack-name jenkins --region us-east-1' 
    }
    }
}
