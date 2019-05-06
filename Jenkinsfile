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
        junit 'reports/*.xml'
    }
}
