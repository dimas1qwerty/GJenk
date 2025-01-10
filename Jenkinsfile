pipeline {
   agent any
   stages {
       stage('Update System') {
           steps {
               sh '''
               sudo apt update
               sudo apt install -y apache2
               '''
           }
       }
       stage('Start Apache') {
           steps {
               sh '''
               sudo systemctl start apache2
               echo "Apache2 Installed and Running" | sudo tee /var/www/html/index.html > /dev/null
               '''
           }
       }
       stage('Check Logs for Errors') {
           steps {
               sh '''
               if [ -f /var/log/apache2/access.log ]; then
                   grep -E "4[0-9]{2}|5[0-9]{2}" /var/log/apache2/access.log || echo "No 4xx or 5xx errors found"
               else
                   echo "Log file does not exist"
               fi
               '''
           }
       }
   }
}
