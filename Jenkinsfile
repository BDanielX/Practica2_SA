//Este archivo lo usa el pipeline de jenkins  prueba
pipeline {
    agent {
        label 'master'
    }

        stages {
        stage("Comprobando funcionamiento de jenkins P2"){
                steps {
                    script {			
                        sh "echo \"Current workspace is $WORKSPACE\""
                    }
                }   
            }

        stage("Actualizar paquetes"){
            steps {
                script {	
                    sh '''cd frontend
                        npm install'''
                }
            }   
        }

        stage("Ejecutar pruebas unitarias"){
            steps {
                script {	
		            sh '''cd frontend
			    	        export CHROME_BIN='/usr/bin/chromium'
                        	ng test --watch=false --browsers=ChromeHeadless'''
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