pipeline {
  agent any
  /*
  tools {
    // Install the Maven version configured as "M3" and add it to the path.
    maven "M3"
  }
  */
  stages {
    /*
    stage('Clean') {
    	steps {
	      sh "rm -rf ejemplo-maven"
	    }
    }
    stage('Clone') {
    	steps {
	      sh "git clone https://github.com/hernanBeiza/ejemplo-maven.git"
	      // mvn 'clean install'
	      // Run Maven on a Unix agent.
	      // sh "mvn -Dmaven.test.failure.ignore=true clean package"
	      // To run Maven on a Windows agent, use
	      // bat "mvn -Dmaven.test.failure.ignore=true clean package"    		
    	}
    }
    */
    stage('Compile') {
    	steps {
	    	echo "Compilar código"
	      //sh "cd ejemplo-maven && ls && ./mvnw clean compile -e"
	      sh "ls && ./mvnw clean compile -e"
	    }
    }
    /*
    stage('Test') {
    	steps {
	    	echo "Testear código"
	    	//sh "cd ejemplo-maven && ./mvnw clean test -e"
	    	sh "./mvnw clean test -e"
	    }
    }
    */
    stage('Jar') {
    	steps {
	    	echo "Generar JAR"
	    	//sh "cd ejemplo-maven && ./mvnw clean package -e"
	    	sh "./mvnw clean package -e"
  	  }
    }
    stage('Sonar') {
    	steps {
	    	echo "Análisis Sonar"
		    //Usar el nombre del sonarqube server configurado en Jenkins
		    withSonarQubeEnv('sonar-scanner') {
		      sh './mvnw org.sonarsource.scanner.maven:sonar-maven-plugin:3.7.0.1746:sonar'
	    	}
	    }
    }
    stage('Run') {
    	steps {
	    	echo "Ejecutar JAR"
	    	//sh "cd ejemplo-maven && nohup bash mvnw spring-boot:run &"
	    	sh "nohup bash mvnw spring-boot:run &"
  	  }
	  }
    stage('TestApp') {
    	steps {
	    	echo "Probar endpoint"
	    	sh "sleep 30 && curl -X GET 'http://localhost:8081/rest/mscovid/test?msg=testing'"
  	  }
	  }
	}
}
