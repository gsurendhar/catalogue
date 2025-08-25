pipeline{
    agent {
        label 'AGENT-1'
    }
    environment{
        appVersion= ''

    }
    options{
        timeout(time:30, unit:'MINUTES')
        disableConcurrentBuilds()
    }
    stages{
        stage('Read package.json'){
            steps{
                script{
                    def packageJSON=readJSON file:'package.json'
                    appVersion=packageJSON.version 
                    echo "package version:${appVersion}"
                }
            }
        }
    }
}