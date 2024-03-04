pipeline {
    agent {
        docker {
            // Menggunakan Docker image 'maven:3.9.0'
            image 'maven:3.9.0'
            // Mengatur volume untuk cache Maven
            args '-v /root/.m2:/root/.m2'
        }
    }
    stages {
        stage('Build') {
            steps {
                // Menjalankan perintah Maven untuk membersihkan dan membangun proyek
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                // Menjalankan perintah Maven untuk menjalankan pengujian
                sh 'mvn test'
            }
            post {
                always {
                    // Menghasilkan laporan pengujian JUnit
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deliver') {
            steps {
                // Menjalankan skrip deliver.sh untuk melakukan pengiriman
                sh './jenkins/scripts/deliver.sh'
            }
        }
    }
}
