pipeline {
    agent {
        label 'master'
    }
    stages {
        stage('Build') {
            steps {
                bat 'mvn -B -DskipTests clean package'
            }
        }
//         stage('Sonar-Report') {
//             steps {
//             sh 'mvn sonar:sonar \
//   -Dsonar.projectKey=jenkins_project \
//   -Dsonar.host.url=http://localhost:9000 \
//   -Dsonar.login=5f09ded7e5db4d0ea0dcfd937c181af706e60475'
//             }
//         }
        stage('Test') { 
            steps {
                bat 'mvn test' 
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml' 
                }
            }
        }
        stage('Sonar-Report') {
    steps {
        bat '''
            @echo off
            REM 1. Set Java to JDK 21 (Required for Sonar Scanner)
            set "JAVA_HOME=C:\\Program Files\\Java\\jdk-21"
            set "PATH=%JAVA_HOME%\\bin;%PATH%"
            
            REM 2. Run the scan with your new Token
            mvn clean install org.sonarsource.scanner.maven:sonar-maven-plugin:3.9.1.2184:sonar -Dsonar.host.url=http://localhost:9000 -Dsonar.analysis.mode=publish -Dsonar.token=squ_3c63024ad504b2be2b8bd99841451530aeb6005d
        '''
    }
}
    }
}
