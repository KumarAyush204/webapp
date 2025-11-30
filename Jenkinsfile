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
            REM Set JAVA_HOME to JDK 21 just for this step
            set "JAVA_HOME=C:\\Program Files\\Java\\jdk-21"
            set "PATH=%JAVA_HOME%\\bin;%PATH%"
            
            REM Verify version (optional, for debugging)
            java -version
            
            REM Run the scan
            mvn clean install org.sonarsource.scanner.maven:sonar-maven-plugin:3.9.1.2184:sonar -Dsonar.host.url=http://localhost:9000 -Dsonar.analysis.mode=publish
        '''
    }
}
    }
}
