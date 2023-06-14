pipeline {
    agent {label "first-slave"}

    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
                withCredentials([usernamePassword(credentialsId: 'iti-sys-admin-mnf-docker-cred', usernameVariable:'username' ,passwordVariable:'password')]) {    // Use the file within the block    echo "File path: ${MY_FILE}"
                sh """
                docker login -u ${username} -p ${password}
                docker build -t mahmoudelsawy2023/testing:v${BUILD_NUMBER} .
                docker push mahmoudelsawy2023/testing:v${BUILD_NUMBER}
                    """
            }
        }
        }
      
        stage('Deployment') {
            steps {
                echo 'Deployment'
                withCredentials([file(credentialsId: 'secret_file_test', variable: 'test')]) {
                sh """
                           mv Deployment/deploy.yaml Deployment/deploy.yaml.tmp
                           cat Deployment/deploy.yaml.tmp | envsubst > Deployment/deploy.yaml
                           rm -rf Deployment/deploy.yaml.tmp
                           kubectl apply -f Deployment/service.yaml --kubeconfig ${test}
                           kubectl apply -f Deployment/deploy.yaml --kubeconfig ${test}
                           
                """
            }
        }
        }       
    }
    
}
