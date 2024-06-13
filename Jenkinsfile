pipeline {
    agent any
    
    parameters {
        choice(name: 'environment', choices: ['staging', 'perf', 'smoke', 'prod'], description: 'Select the environment')
        dynamicReference(
            name: 'regions',
            referencedParameter: 'environment',
            script: '''
                def environmentRegions = [
                    'prod': ['eu-west-1', 'eu-central-1', 'us-east-1', 'us-east-2', 'us-west-2'],
                    'smoke': ['us-east-1', 'us-west-2'],
                    'staging': ['eu-west-1', 'eu-central-1', 'us-east-1', 'us-east-2', 'us-west-2'],
                    'perf': ['us-east-1']
                ]
                return environmentRegions[params.environment]
            ''',
            description: 'Select the region'
        )
        choice(name: 'deployType', choices: ['regular update', 'restart from timestamp'], description: 'Deploy type')
        string(name: 'parallelism', description: 'Parallelism values for each region (comma separated, e.g., 2,3)', trim: true)
        string(name: 'timestamp', description: 'Timestamp for restart (only applicable for restart deploy type)', trim: true)
    }

    stages {
        stage('Initialize') {
            steps {
                script {
                    echo "Environment: ${params.environment}"
                    echo "Regions: ${params.regions}"
                    echo "Deploy Type: ${params.deployType}"
                    echo "Parallelism: ${params.parallelism}"
                    echo "Timestamp: ${params.timestamp}"
                }
            }
        }

        // Add more stages as required
    }
}
