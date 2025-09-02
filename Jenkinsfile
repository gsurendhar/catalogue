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
        stage('Install Dependencies'){
            steps{
                script{
                    sh """
                        npm install
                    """
                }
            }
        }
        stage('Unit Testing'){
            steps{
                script{
                    sh """
                        echo "Unit Tests is going on when we provide test cases"
                    """
                }
            }
        }
        stage('Docker Build'){
            steps{
                script{
                    withAWS(credentials:'AWS-creds', region: 'us-east-1') {
                        sh """
                            echo "ECR BIULD command"
                        """
                    }
                }
            }
        }
        stage('Deploy'){
            input{
                message "should we countinue ?"
                ok "yes,we Should"
                submitter "Mr Jenkins"
                parameters {
                    string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
                }
            }
            steps{
                script{
                    withAWS(credentials:'AWS-creds', region: 'us-east-1') {
                        sh """
                            echo "Deploying"
                            echo "hello, ${PERSON}, nice to meet you"
                        """
                    }
                }
            }
        }
    }
}