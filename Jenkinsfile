#!groovy

def parallel_steps = [:]

def createStep(stepClosures) {
      stage('Prepare Workspace') {
        checkout scm
      }

      stepClosures.each { k, v ->
        stage(k, v)
      }
}

createStep([ 
  'Hello, World': {
    echo "Hello, World"
  }
])

parallel_steps['Hello, Parallel World 1'] = {
  createStep([
    'Parallel World 1': {
     try {
      echo "Parallel World 1"
	  } finally {
        archiveArtifacts allowEmptyArchive: true, artifacts: 'test.log'
      }
    },
  ])
}
parallel_steps['Hello, Parallel World 2'] = {
  createStep([
    'Parallel World 2': {
     try {
      echo "Parallel World 2"
	  } finally {
        archiveArtifacts allowEmptyArchive: true, artifacts: 'test.log'
      }
    },
  ])
}

parallel parallel_steps