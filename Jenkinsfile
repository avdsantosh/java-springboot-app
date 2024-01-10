pipeline {
    agent {
        node {
            label 'jenkins-slave-node'
        }
    }
    environment {
        PATH = "/opt/apache-maven-3.9.6/bin:$PATH"
    }
    stages {
        stage("build"){
            steps {
                echo "build started"
                sh 'mvn clean package -Dmaven.test.skip=true'
                echo "build complted"
            }
        }
    stage('SonarQube analysis') {
            environment {
                scannerHome = tool 'sonar-scanner-portal'
            }
            steps{
                withSonarQubeEnv('sonar-server-portal') {
                    sh "${scannerHome}/bin/sonar-scanner"
                }
            }
        }
    }
}
    
    