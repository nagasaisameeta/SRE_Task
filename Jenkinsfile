node{

                 stage('Clone repo'){
                 git branch: 'main', credentialsId: 'Githubcredentials', url: 'https://github.com/Ravitejano1/SRE_Task.git'
                }

                stage('Maven Build'){
                def mavenHome = tool name: "Maven-3.8.6", type: "maven"
                def mavenCMD = "${mavenHome}/bin/mvn"
                sh "${mavenCMD} clean package"
                }

                stage('SonarQube analysis') {
                withSonarQubeEnv('Sonar-Server-7.8') {
                def mavenHome = tool name: "Maven-3.8.6", type: "maven"
                def mavenCMD = "${mavenHome}/bin/mvn"
                sh "${mavenCMD} sonar:sonar"
                }
        }

                stage('upload war to nexus'){
                        nexusArtifactUploader artifacts: [
                        [
                                artifactId: 'raviproject',
                                classifier: '',
                                file: 'target/raviproject.war',
                                type: 'war'
                                ]
                        ],
                                credentialsId: 'nexus',
                                groupId: 'in.ravi',
                                nexusUrl: 'http://54.221.191.23:8081/repository/Sidgsrelease/',
                                nexusVersion: 'nexus3',
                                repository: 'Sidgsrelease/',
                                protocol: 'http',
                                version: '2.0.0'
                        }
        }
