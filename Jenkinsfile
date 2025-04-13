pipeline {
    agent any

    stages {
        stage('Install Apache') {
            steps {
                sh '''
                    sudo apt-get update
                    sudo apt-get install -y apache2
                '''
            }
        }

        stage('Check Apache logs for 4xx/5xx') {
            steps {
                sh '''
                    LOG_PATH="/var/log/apache2/access.log"
                    if [ -f "$LOG_PATH" ]; then
                        echo "Checking for 4xx and 5xx errors in logs..."
                        grep -E "HTTP/1.[01]\" [45][0-9]{2}" $LOG_PATH || echo "No 4xx/5xx errors found."
                    else
                        echo "Log file not found: $LOG_PATH"
                    fi
                '''
            }
        }
    }
}
