pipeline {
    agent any

    stages {
  	stage('Checkout') {
	    steps {
		// Clona repo de git :)
		git 'https://github.com/pablonssss/repojenkins'
	    }
	}

	stage('Build') {
	    steps {
		// Hacemos de cuenta que vamos a compilar un proyecto...
		echo 'Compilandooo'
		// Aqui agregamos comandos para realizar una compilacion
	    }
   	}

	stage('Test') {
	    steps {
		// Ejecucion de pruebas
		echo 'Probandooo'
		// Aca comandos que realmente ejecuten pruebas
	    }
	}

	stage('Archive artefacts') {
	    steps {
		// Archivando artefacto que genero la compilacionnn
		echo 'Archivandooo'
	    }
   	}
    }

    post {
	success {
	    echo 'Pipeline exitoso'
	}
	failure {
	    echo 'Pipeline fallo'
	}
    }
}
