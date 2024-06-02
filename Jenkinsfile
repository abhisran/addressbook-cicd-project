pipeline {
    agent any  
    stages {
        stage("Checkout Git") {
            steps {
                echo "Checking out Git repository..."
                git url: "https://github.com/abhisran60/addressbook-cicd-project.git"
            }
        }

        stage("Compile Code") {
            steps {
                echo "Compiling code..."
                sh "mvn compile"
            }
        }

        stage("Testing the code") {
            steps {
                echo "Maven Test..."
                sh "mvn test"
            }
        }

        stage("QA for the Code") {
            steps {
                echo "QA being done for the code..."
                sh "mvn checkstyle:checkstyle"
                recordIssues sourceCodeRetention: 'LAST_BUILD', tools: [checkStyle()]
            }
        }

        stage("Converting the code to package") {
            steps {
                echo "Packaging being done..."
                sh "mvn package"
            }
        }

        stage('Deploy') {
            steps {
                sh "cp /var/lib/jenkins/workspace/addressbook-cicd-project/target/addressbook.war /opt/apache-tomcat-8.5.100/webapps/addressbook.war"
                echo "Successfully deployed addressbook.war with apache tomcat"
            }
        }
    }
}
