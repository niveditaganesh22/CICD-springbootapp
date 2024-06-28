pipeline{
    agent any
    tools{
        maven Maven-Jenkins
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
        
    }
}