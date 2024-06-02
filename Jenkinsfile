pipeline {
    agent any
    stages {
        stage ("Git Checkout") {
            steps {
                git url: "https://github.com/abhisran60/addressbook-cicd-project.git"
                echo "Git checkout done"
            }
        }
        stage ("Build") {
            steps {
                sh "mvn clean install"
                echo "Build done"
        }
        stage ("Test") {
            steps {
                sh "mvn test"
                echo "Test done"
            }
        }
        stage ("QA") {
            steps {
                sh "mvn checkstyle:checkstyle"
                recordIssues sourceCodeRetention: 'LAST_BUILD', tools: [checkStyle()]
                echo "QA done"
            }
        }
        stage ("Package") {
            steps {
                sh "mvn package"
                echo "Package done"
            }
        }
        stage ("Deploy") {
            steps {
                sh "cp /var/lib/jenkins/workspace/addressbook-cicd-project/target/addressbook.war /opt/apache-tomcat-8.5.100/webapps/addressbook.war"
                echo "Successfully deployed addressbook.war with apache tomcat"
            }
        }
    }
}