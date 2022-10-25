pipeline {
  agent {
     node { 
        label 'CONBSW10VM028'
        } 
  }
  stages {
    stage('No Converter-0') {
      steps {
        echo 'No converter for Builder: hudson.plugins.powershell.PowerShell'
      }
    }

    stage('Maven Build 0') {
      steps {
        sh 'mvn -B -ntp clean'
      }
    }

    stage('No Converter-1') {
      steps {
        echo 'No converter for Builder: hudson.tasks.Ant'
      }
    }

    stage('Maven Build 1') {
      steps {
        sh 'mvn -B -ntp clean deploy -PbuildExtras -U -f projects/papoyan-install4j-zip/pom.xml maven1.home=C:/fbcdev/thirdparty/apache/maven/maven-1.1'
      }
    }

    stage('Maven Build 2') {
      steps {
        sh 'mvn -B -ntp deploy -Pdb-mysql -Ddlls -U maven1.home=C:/fbcdev/thirdparty/apache/maven/maven-1.1'
      }
    }

    stage('Maven Build 3') {
      steps {
        sh 'mvn -B -ntp clean deploy -Droot.dir=. -f projects/papoyan-install4j-installer/pom.xml'
      }
    }

  }
  tools {
    maven 'Maven 3.6.3'
    jdk 'OpenJDK 1.8.0_322 WIN64'
  }
  post {
    always {
      step($class: 'ArtifactArchiver', artifacts: 'koko/dev/projects/fbc-build-all/target/databaseDump/load*.txt')
      echo 'No converter for Publisher: hudson.plugins.chucknorris.CordellWalkerRecorder'
      echo 'No converter for Publisher: hudson.plugins.claim.ClaimPublisher'
      echo 'No converter for Publisher: hudson.plugins.emailext.ExtendedEmailPublisher'
    }

  }
  options {
    buildDiscarder(logRotator(daysToKeepStr: '150', numToKeepStr: '300'))
  }
  triggers {
    cron('''# morning demand 5:30am 
H 5 * * *''')
  }
}
