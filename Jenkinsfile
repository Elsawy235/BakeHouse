pipeline {
    agent {label "first-slave"}

    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
                withCredentials([usernamePassword(credentialsId: 'iti-sys-admin-mnf-docker-cred', usernameVariable:'username' ,passwordVariable:'password')]) {    // Use the file within the block    echo "File path: ${MY_FILE}"
                sh """
                docker login -u ${username} -p ${password}
                docker build -t mahmoudelsawy2023/mahmoud:v1 .
                docker push mahmoudelsawy2023/mahmoud:v1
                    """
            }
        }
        }
        stage('Build') {
            steps {
                echo 'Build'
                sh "ls"
            }
        }
        stage('Deployment') {
            steps {
                echo 'Deployment'
                sh "ls"
            }
        }
            
    }
    
}
