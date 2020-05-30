buildPluginWithGradle()
node {
    notify("Started")
    
    try {
        stage("checkout") {
			checkout scm
        }
        
        dir("jenkins-gradle-sonarqube-example") {
            stage("build") {
                withSonarQubeEnv("Sonarqube Server") {
					withGradle(installation: "Gradle Installation") {
					    sh "chmod +x ./gradlew"
						sh "./gradlew build sonarqube"
					}
                }
            }
            
            //stage("archival") {
            //    archiveArtifacts "target/*.?ar"
            //}
        }
        
        notify("Success")
    } catch (err) {
        notify("Error ${err}")
        currentBuild.result = "FAILURE"
    }
}
