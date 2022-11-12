import groovy.json.JsonSlurperClassic

def jsonParse(def json) {
    new groovy.json.JsonSlurperClassic().parseText(json)
}

def COLOR_MAP = [ 
    'SUCCESS' : 'GOOD', 
    'FAILURE' : 'DANGER' 
]

def getBuildUser(){ 
    return currentBuild.rawBuild.getCause(Cause.UserIdCause).getUserId() 
}

pipeline {
    agent any
    
    enviroment{ 
        BUILD_USER = '' 
    }
    
    stages {
        stage("Saludar"){
            steps {
                script {
                sh "echo 'Hello, World Usach!'"
                }
            }
        }
        stage("Sonar: Análisis SonarQube"){
            steps {
                sh "echo 'Calling sonar Service in another docker container!'"
                // Run Maven on a Unix agent to execute Sonar.
                sh './mvnw clean verify sonar:sonar'
            }
        }
    }
    post {
        always {
            script{ 
                BUILD_USER = getBuildUser() 
            }

            slackSend channel: 'jen-example' color : COLOR_MAP[currentBuild.currentResult], message: "{currentBuild.currentResult}: Job {env.BUILD_NUMBER} by {SPEC} at {env.BUILD_URL}HTML_20Report/"
            
            sh "echo 'fase always executed post'"
        }
        success {
            sh "echo 'fase success'"
        }
        failure {
            sh "echo 'fase failure'"
        }
    }
}
