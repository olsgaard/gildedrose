node {
    stage('checkout'){
        sh "echo $PWD"
        checkout([$class: 'GitSCM', branches: [[name: '*/master']], 
            doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], 
            userRemoteConfigs: [[credentialsId: '8a5c5968-0508-4d5b-b6e5-819fd464435f', 
                url: 'https://github.com/olsgaard/gildedrose']]]
        )
    }
    stage('build'){
        //sh 'docker run -i --rm --name my-maven-project -v "$PWD":/usr/src/mymaven -w /usr/src/mymaven maven:3-jdk-8 mvn test'
        sh 'docker run -i --rm --name my-maven-project -v "$PWD":/usr/src/mymaven -w /usr/src/mymaven maven:3-jdk-8 mvn install'

    }
    stage('junit'){
        junit '**/target/surefire-reports/TEST-*.xml'
    }
    stage('archive'){
        archiveArtifacts 'target/gildedrose-*.jar'
    }
}
