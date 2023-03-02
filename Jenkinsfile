pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
		sh 'dotnet build'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
		sh 'dotnet test'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
		sh 'dotnet publish KinoServerBackend/KinoServerBackend.csproj -c Release -r linux-x64 --self-contained'
		sh 'ls KinoServerBackend/bin/Release/net6.0/linux-x64/publish/'
		ftpPublisher alwaysPublishFromMaster: false, continueOnError: false, failOnError: false, masterNodeName: 'master', paramPublish: [parameterName: ''], publishers: [
			[configName: 'Backend deploy', transfers: [
				[asciiMode: false, cleanRemote: false, excludes: '', flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '~/API/', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '/var/lib/jenkins/workspace/KinoServeBackend/KinoServerBackend/bin/Release/net6.0/linux-x64/publish/**']
			], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false]
		]
            }
        }
    }
}
