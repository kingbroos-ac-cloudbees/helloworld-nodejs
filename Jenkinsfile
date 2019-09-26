#!groovy
def parallel_steps = [:]

// Create a single step for running. Currently runs on just 1 node
def createStep(stepClosures, node_label = null) {
	node(node_label) {
      stepClosures.each { k, v ->
        stage(k, v)
      }
	}
}

// Define parallel steps, because reasons
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

// ACTUAL PIPELINE
createStep([
	'Prepare Workspace': {
		checkout scm
	},
	'Hello, World': {
		echo "Hello, World!"
		sh 'java -version'
	}
])

parallel parallel_steps