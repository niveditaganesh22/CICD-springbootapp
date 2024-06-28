pipeline{
    agent any
    tools{
        maven Maven-Jenkins
    }
    environment {
        SCANNER_HOME= tool 'Sonar-Scanner'
    }
    stages{
        stage('Git checkout'){
            steps{
                git branch: 'main', url:'https://github.com/niveditaganesh22/CICD-springbootapp.git'
            }
        }
        stage('Maven Build'){
            steps{
                sh 'mvn clean install'
            }
        }
        stage('Unit Test') {
            steps {
                echo '<----------------------Unit Test Under Progess-------------------->'
                sh 'mvn surefire-report:report'
                echo '<----------------------Unit Test Finished------------------------->'
            }
        }
        stage('SonarQube Analysis') {
            steps {
               script {
                withSonarQubeEnv('sonar-server') {
                sh ''' $SCANNER_HOME/bin/Sonar-Scanner -Dsonar.projectName=CICD-springbootapp -Dsonar.projectKey=niveditaganesh22_CICD-springbootapp '''
                }
               }
            }
        }
    //     stage ('Quality Gate'){
    //         steps {
    //            script {
    //             waitForQualityGate abortPipeline: false, credentialsId: 'sonar'
    //         }
    //     }
    //   }
        


    }
}