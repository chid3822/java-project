properties([pipelineTriggers([githubPush()])]) 

node('linux'){
    stage('Unit Tests'){
        git "https://github.com/chid3822/java-project.git"
        sh "ant -f test.xml -v"
        junit 'reports/result.xml'
    }
    stage('Build'){
        sh "ant -f build.xml -v"
    }
    
    stage('Deoply'){
        sh "ant -buildfile test.xml"
    }
    
    stage('Report'){
       withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: '', credentialsId: '14dd1bff-3295-4649-a919-3fc6ad57f627', secretKeyVariable: '']]) { 
           sh 'aws cloudformation describe-stack-resources --region useast-1 --stack-name jenkins'
       }
    }
}
