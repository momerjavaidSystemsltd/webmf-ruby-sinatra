node('docker') {
  checkout scm
  def ruby = docker.image('ruby')

  stage('Build') {
    ruby.inside {
      sh 'bundle install'
    }
  }
  
  try {
    stage('Test') {
      ruby.inside {
        sh 'rake ci:all'
      }
    }
  } catch (e) {
    echo 'Tests have failed!'
  } finally {
    ruby.inside {
      junit 'test/reports/TEST-AppTest.xml'
    }
  }
}

