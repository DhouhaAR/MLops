pipeline {
 
 agent any
     
    stages {
        stage('Getting Project from Git') {
            steps {
                echo 'Project is downloading...'
                git branch:'main', url:'https://github.com/DhouhaAR/MLops.git'
  
                 }
             }
          stage('Building docker container') {
            steps {
                  bat 'docker build -t diabetes-model .'
                  bat 'docker run -d --name model1 diabetes-model'
               }
           }
            stage('Preprocessing stage') {
            steps {
                   bat 'docker container exec model1 python3 preprocessing.py'
               }
           }
           stage('Training stage') {
            steps {
                    bat 'docker container exec model1 python3 train.py'
                }
        }
        stage('Test stage') {
              steps {
                    bat 'docker container exec model1 python3 train.py'
                    bat 'docker container exec model1 python3 test.py'
                    bat 'docker container exec model1 cat /home/jovyan/results/train_metadata.json /home/jovyan/results/test_metadata.json' 
                    bat 'docker rm -f model1'
                  }
               }
    }
}
