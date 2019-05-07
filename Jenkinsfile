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
     
    stage('Report'){
        withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'assign10real', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
            sh 'aws cloudformation describe-stack-resources --region useast-1 --stack-name week10'
       }
    }
}
