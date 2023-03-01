node{

                 stage('Clone repo'){
                 git branch: 'main', credentialsId: 'Githubcredentials', url: 'https://github.com/nagasaisameeta/SRE_Task.git'
                }

                stage('Maven Build'){
                def mavenHome = tool name: "Maven-3.6.3", type: "maven"
                def mavenCMD = "${mavenHome}/bin/mvn"
                sh "${mavenCMD} clean package"
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
                                nexusUrl: 'http://54.237.223.51:8081/repository/sairelease/',
                                nexusVersion: 'nexus',
                                repository: 'sairelease/',
                                protocol: 'http',
                                version: '2.0.0'
                        }
        }
