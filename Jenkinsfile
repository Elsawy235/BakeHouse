pipeline {
    agent {label "node-slave"}
      stages{
          stage('build'){
              steps {
                  
                      echo "build"
                  withCredentials([usernamePassword(credentialsId: 'dockerhub_credential', usernameVariable: 'USERNAME',passwordVariable: 'PASSWORD')]){
                      sh '''
                  docker login -u ${USERNAME} -p ${PASSWORD}
                  docker build -t mahmoudelsawy2023/bakehouseitisysadmin:v${BUILD_NUMBER} .
                  docker push mahmoudelsawy2023/bakehouseitisysadmin:v${BUILD_NUMBER}
                  
                  '''
                  }
              }
      }
           stage('deploy'){
              steps {
                  echo "deploy"
                  sh ' ls '
                  }
              }
      }
        
}
   /* parameters {
    choice(name: 'ENV_ITI', choices: ['dev','test','prod','release'])
    }

    stages {
        stage('Build') {
            steps {
                script{ 
                    echo 'Build'
                    if (params.ENV_ITI=="release"){
                        withCredentials([usernamePassword(credentialsId: 'iti-sys-admin-mnf-docker-cred', usernameVariable:'username' ,passwordVariable:'password')]) {    // Use the file within the block    echo "File path: ${MY_FILE}"
                        sh '''
                        docker login -u ${username} -p ${password}
                        docker build -t mahmoudelsawy2023/testing:v${BUILD_NUMBER} .
                        docker push mahmoudelsawy2023/testing:v${BUILD_NUMBER}
                        echo ${BUILD_NUMBER} > ../build_num.txt
                        echo ${ENV_ITI}
                            '''
                        }
                    }
                    else{
                        echo "user chose ${params.ENV_ITI}"
                    }
            }
        }
        }
      
        stage('Deployment') {
            steps {
                echo 'Deployment'
                script{
                    if (params.ENV_ITI== "dev" || params.ENV_ITI== "prod" || params.ENV_ITI== "test"){
                        withCredentials([file(credentialsId: 'secret_file_test', variable: 'test')]) {
                        sh '''
                           export BUILD_NUMBER=$(cat ../build_num.txt)
                           mv Deployment/deploy.yaml Deployment/deploy.yaml.tmp
                           cat Deployment/deploy.yaml.tmp | envsubst > Deployment/deploy.yaml
                           rm -rf Deployment/deploy.yaml.tmp
                           kubectl apply -f Deployment/service.yaml --kubeconfig ${test} -n ${ENV_ITI}
                           kubectl apply -f Deployment/deploy.yaml --kubeconfig ${test} -n ${ENV_ITI}
                           
                            '''
                             }
                    
                    }
                    else{
                         echo "user chose ${params.ENV_ITI}"
                    }
                    
                }
                
        }
        }       
    }
    
}
*/
