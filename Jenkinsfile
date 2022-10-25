pipeline {
  agent {
     node { 
        label 'CONBSW10VM027'
        } 
  }
  stages {
    stage('No Converter-0') {
      steps {
        echo 'No converter for Builder: hudson.tasks.Ant'
      }
    }

  }
  post {
    always {
      step(checksName: 'Tests', testDataPublishers: [{$class=ClaimTestDataPublisher}], $class: 'JUnitResultArchiver', testResults: 'koko\\dev\\projects\\*\\target\\test-reports\\TEST*.xml,koko\\dev\\plugins\\projects\\*\\target\\test-reports\\TEST*.xml')
      echo 'No converter for Publisher: hudson.plugins.claim.ClaimPublisher'
      echo 'No converter for Publisher: hudson.plugins.emailext.ExtendedEmailPublisher'
    }

  }
  options {
    buildDiscarder(logRotator(daysToKeepStr: '120', numToKeepStr: '120'))
  }
  triggers {
    pollSCM('H/10 4-20 * * *')
  }
}
