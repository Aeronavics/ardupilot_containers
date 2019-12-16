pipeline {
  agent any
  stages {
    stage('build_images') {
      environment{
          AERONAVICS_REGISTRY_CREDS = credentials('aeronavics_registry_user')
          QGC_NEXUS_CREDS = credentials('qgc_uploader')
      }
      parallel {
        stage('build_containers') {
          steps {
            sh 'docker build . -t pelardon.aeronavics.com:8083/ardupilot_container:latest'
            sh 'docker login pelardon.aeronavics.com:8083 --username ${AERONAVICS_REGISTRY_CREDS_USR} --password ${AERONAVICS_REGISTRY_CREDS_PSW}'
            sh 'docker push pelardon.aeronavics.com:8083/ardupilot_container:latest'
          }
        }
      }
    }
  }
}
