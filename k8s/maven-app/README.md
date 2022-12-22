this is a simple java maven application. 


pipeline{
    agent any
    tools{
        maven "maven"
    }
    environment{
        registry = "public.ecr.aws/z2t0b6v5/maven-artifact"
    }
    stages{
        stage ('SCM checkout'){
            steps{
                git branch: 'main', url: 'https://github.com/comrider/springboot-app.git'
            }
        }
        stage('build jar file'){
            steps{
                sh 'mvn clean install '
            }
        }
        stage('buid docker image'){
            steps{
                script {
                    docker.build registry                 
                }
            }
        }
        stage ('Push into ECR'){
            steps{
                sh 'aws ecr-public get-login-password --region us-east-1 | docker login --username AWS --password-stdin public.ecr.aws/z2t0b6v5'
                sh 'docker push public.ecr.aws/z2t0b6v5/maven-artifact:latest'
            }
        }
        stage ('deploying the spring boot application in k8s'){
            steps{
                withKubeConfig(caCertificate: '', clusterName: '', contextName: '', credentialsId: 'istio-secret-file', namespace: '', serverUrl: '') {
                    sh 'kubectl apply -f eks-deploy-k8s.yaml'
                }
            }
        }
    }
}