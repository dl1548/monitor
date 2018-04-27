//Jenkinsfile (Declarative Pipeline)//
pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                sh 'pwd'
                sh 'mvn clean install -f moni/pom.xml'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
                sh 'pwd'
                //sh 'mvn clean verify sonar:sonar -f moni/pom.xml'//
            }
        }
        stage('Deploy') {
            steps {
                echo 'upload file to server....'
                sh "sshpass -p centos scp $WORKSPACE/moni/target/monitor.war root@192.168.1.55:/root/war"
                echo 'Restart tomcat.....'
                sh "sshpass -p centos ssh root@192.168.1.55 '/usr/bin/bash ~/deploy.sh monitor 80 /usr/local/tomcat-7.0.85 $BUILD_NUMBER'"
            }
        }
    }
}
