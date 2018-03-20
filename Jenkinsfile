pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                echo 'Checkout'
		
            }
        }
        stage('Build') {
            steps {
                echo 'Clean Build'
		withEnv(["JAVA_HOME=${ tool 'jdk1.8.0_144' }", "PATH+MAVEN=${tool 'maven-3.5.0'}/bin:${env.JAVA_HOME}/bin"]) {

                bat 'mvnw clean compile'
		}
            }
        }
        stage('Test') {
            steps {
                echo 'Testing'
                bat 'mvnw test'
            }
        }
        stage('JaCoCo') {
            steps {
                echo 'Code Coverage'
                jacoco()
            }
        }
        stage('Sonar') {
            steps {
                echo 'Sonar Scanner'
               //def scannerHome = tool 'SonarQube Scanner'
		withSonarQubeEnv('SonarQube Server') {
		bat '$(scannerHome)/bin/sonar-scanner'
		 }
            }
        }
        stage('Package') {
            steps {
                echo 'Packaging'
                bat 'mvnw package -DskipTests'
            }
        }
        stage('Deploy') {
            steps {
                echo '## TODO DEPLOYMENT ##'
            }
        }
    }
    
    post {
        always {
            echo 'JENKINS PIPELINE'
        }
        success {
            echo 'JENKINS PIPELINE SUCCESSFUL'
        }
        failure {
            echo 'JENKINS PIPELINE FAILED'
        }
        unstable {
            echo 'JENKINS PIPELINE WAS MARKED AS UNSTABLE'
        }
        changed {
            echo 'JENKINS PIPELINE STATUS HAS CHANGED SINCE LAST EXECUTION'
        }
    }
}
