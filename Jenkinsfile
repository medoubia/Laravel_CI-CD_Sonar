pipeline {
    agent any


    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/medoubia/Laravel_CI-CD_Sonar.git', branch: 'main'
            }
        }

        stage('Install Deps') {
            steps {
                // sh 'composer install'
                echo 'composer install'
            }
        }
        
        stage('Build Laravel') {
            steps {
                // script {
                //     sh 'php artisan serve &'
                // }
                echo 'php artisan serve &'
            } 
        } 

        stage('installer les dépendances Node') {
            steps {
                // script {
                //     sh 'npm install'
                // }
                echo 'npm install'
            }
        }

        stage('compiler les assets Node') {
            steps { 
                // script {
                //     sh 'npm run build'
                // }
                echo 'npm run build'
            } 
        }

        // stage('SonarQube Analysis') {
        //     steps {
        //         withSonarQubeEnv('SonarQube') {
        //             sh 'docker run --network=host -e SONAR_HOST_URL="http://127.0.0.1:9000" -v "$PWD:/usr/src" sonarsource/sonar-scanner-cli'
        //         }
        //     }
        // }

        // stage('SonarQube Analysis') {
        //     steps {
        //         script {
        //             def scannerHome = tool 'sonar-scanner'
        //             withSonarQubeEnv('SonarQube') {
        //                 sh """
        //                     ${scannerHome}/bin/sonar-scanner \
        //                     -Dsonar.projectKey=GitlabMx \
        //                     -Dsonar.host.url=http://localhost:9000 \
        //                     -Dsonar.login=sqp_5c7cf314cd19d3f60ed624ea584d547820ccd482 \
        //                     -Dsonar.sources=./app \
        //                     -Dsonar.exclusions="vendor/*,storage/**,bootstrap/cache/*"
        //                 """
        //             }
        //         }
        //     }
        // }


        // stage('Quality Gate') {
        //     steps {
        //         timeout(time: 5, unit: 'MINUTES') {
        //             waitForQualityGate abortPipeline: true
        //         }
        //     }
        // }

        // stage('Email Sent') {
        //     steps{
        //         sh 'swaks --to houcine.chakra10@gmail.com \
        //             --from "chakra.hs.business@gmail.com" \
        //             --server "smtp.gmail.com" \
        //             --port "587" \
        //             --auth PLAIN \
        //             --auth-user "chakra.hs.business@gmail.com" \
        //             --auth-password "pnuw lgzu ofkv oyoq" \
        //             --helo "localhost" \
        //             --tls \
        //             --data "Subject: Sonar Subject Test\n\nSalam charaf from CLI"'
        //     }
        // }
    }

    post {
        always {
            echo "Analyse terminée, vérifiez SonarQube pour les résultats."
        }

        failure {
            script {
                emailext(
                    subject: "Pipeline Failed: ${env.JOB_NAME} ${env.BUILD_NUMBER}",
                    body: """<p>Bonjour,</p>
                             <p>Le pipeline <strong>${env.JOB_NAME}</strong> a échoué à l'étape de Quality Gate lors de l'exécution de la build numéro <strong>${env.BUILD_NUMBER}</strong>.</p>
                             <p>Statut de la Quality Gate: <strong style="color: red;">${currentBuild.result}</strong></p>
                             <p>Vérifiez les détails de la build ici : <a href="${env.BUILD_URL}">${env.BUILD_URL}</a></p>
                             <p>Cordialement,</p>
                             <p>Votre serveur Jenkins</p>""",
                    // to: 'houcine.chakra10@gmail.com', // Remplacez par les adresses souhaitées
                    // from:"chakra.hs.business@gmail.com",
                    // replyTo:"chakra.hs.business@gmail.com",
                    mimeType: 'text/html'
                )
            }
        }

        success {
            script {
                emailext(
                    subject: "Pipeline Succeeded: ${env.JOB_NAME} ${env.BUILD_NUMBER}",
                    body: """<p>Bonjour,</p>
                             <p>Le pipeline <strong>${env.JOB_NAME}</strong> s'est terminé avec succès à l'étape de Quality Gate lors de l'exécution de la build numéro <strong>${env.BUILD_NUMBER}</strong>.</p>
                             <p>Statut de la Quality Gate: <strong style="color: green;">${currentBuild.result}</strong></p>
                             <p>Vérifiez les détails de la build ici : <a href="${env.BUILD_URL}">${env.BUILD_URL}</a></p>
                             <p>Cordialement,</p>
                             <p>Votre serveur Jenkins</p>""",
                    // to: 'houcine.chakra10@gmail.com', // Remplacez par les adresses souhaitées
                    // from:"chakra.hs.business@gmail.com",
                    // replyTo:"chakra.hs.business@gmail.com",
                    mimeType: 'text/html'
                )
            }
        }
    }
}
