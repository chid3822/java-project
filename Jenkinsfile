properties([pipelineTriggers([githubPush()])]) 
node('linux'){
    stage('Unit Tests'){
        git 'https://github.com/chid3822/java-project.git'
        sh 'ant -f test.xml -v\'
        junit 'reports/result.xml'
    }
    stage('Build'){
        sh 'ant -f build.xml -v'
    }
    stage('Deoply'){
        sh 'cp https://github.com/chid3822/java-project/blob/master/build.xml/rectangle-${env.BUILD_NUMBER}.jar https://s3.console.aws.amazon.com/s3/buckets/chid3822-assignment-4/'
    }
    
    stage('Report'){
       withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: '', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
       // some block 
            sh 'aws cloudformation describe-stack-resources --region useast-1 --stack-name jenkins'
       
       }
    }
}
