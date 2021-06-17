//Este archivo lo usa el pipeline de jenkins  prueba
pipeline {
    agent {
        label 'master'
    }

        stages {
        stage("Ansible Frontend"){
                steps {
                    ansiblePlaybook credentialsId: 'ubuntu', disableHostKeyChecking: true, installation: 'Ansible_Practica2', inventory: 'inventory.inv', playbook: 'playbook-frontend.yml'
                }   
            }
        
        stage("Ansible Backend"){
                steps {
                    ansiblePlaybook credentialsId: 'ubuntu', disableHostKeyChecking: true, installation: 'Ansible_Practica2', inventory: 'inventory.inv', playbook: 'playbook-backend.yml'
                }   
            }

        stage("Actualizar paquetes frontend"){
            steps {
                script {	
                    sh '''cd frontend
                        npm install'''
                }
            }   
        }

        stage("Actualizar paquetes backend"){
            steps {
                script {	
                    sh '''cd backend
                        npm install'''
                }
            }   
        }
	
	stage("Realizo build"){
                steps {
                    script {			
                        sh '''cd frontend
	                    ng build
        	            cd dist
                        cd frontend
                        mv * /var/www/html'''
                    }
                }   
            }
    }

    post { 
        always {          
            deleteDir()
            sh "echo 'Entra en always'"
        }
        success {
            sh "echo 'Entra en success'"
        }
        failure {
            sh "echo 'Entra en failure'"
        }   
    }
}