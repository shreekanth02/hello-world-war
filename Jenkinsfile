pipeline {
    agent {label 'slave1'}
    stages {
        stage('my Build') {
            steps {
                sh "echo ${BUILD_VERSION}"
                sh 'docker build -t tomcat_build:${BUILD_VERSION} .'
            }
        }  
        stage('publish stage') {
            agent {label 'slave1'}
            steps {
                sh "echo ${BUILD_VERSION}"
                withCredentials([usernamePassword(credentialsId: 'Dockerhub', passwordVariable: 'Dockerhubpassword', usernameVariable: 'DockerhubUser')]) {
                sh 'docker login -u${env.DockerhubUser}  -p ${env.Dockerhubpassword}'
                sh 'docker tag tomcat_build:${BUILD_VERSION} shree02/mytomcat:${BUILD_VERSION}'
                sh 'docker push shree02/mytomcat:${BUILD_VERSION}'
            }
        } 
        stage( 'my deploy' ) {
        agent {label 'slave2'} 
            steps {
               sh 'docker rm -f mytomcat'
               sh 'docker run -d -p 8080:8080 --name mytomcat shree02/mytomcat:${BUILD_VERSION}'
            }
        }    
    } 
}
