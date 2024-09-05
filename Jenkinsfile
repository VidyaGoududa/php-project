pipeline {
    agent any
    stages{
        stage('git cloned'){
            steps{
                git url:'https://github.com/VidyaGoududa/php-project/', branch: "master"
              
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t vidyagouda/akshatnewimg6july:v1 .'
                    sh 'docker images'
                }
            }
        }
          stage('Docker login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerjenkin', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                    sh "echo $PASS | docker login -u $USER --password-stdin"
                    sh 'docker push vidyagouda/akshatnewimg6july:v1'
                }
            }
        }
        
     stage('Deploy') {
            steps {
               script {
                   def dockerrm = 'sudo docker rm -f My-first-containe2211 || true'
                    def dockerCmd = 'sudo docker run -itd --name My-first-containe2211 -p 8083:80 vidyagouda/akshatnewimg6july:v1'
                    sshagent(['sshkeypair']) {
                        //chnage the private ip in below code
                        // sh "docker run -itd --name My-first-containe2111 -p 8083:80 vidyagouda/2febimg:v1"
                         sh "ssh -o StrictHostKeyChecking=no ubuntu@3.110.154.121 ${dockerrm}"
                         sh "ssh -o StrictHostKeyChecking=no ubuntu@3.110.154.121 ${dockerCmd}"
                    }
                }
            }
        }
    }
}
