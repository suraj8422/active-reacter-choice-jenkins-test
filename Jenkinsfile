pipeline {
    agent any
    
    parameters {
        choice(
            name: 'environment',
            choices: ['staging', 'perf', 'smoke', 'prod'],
            description: 'Select the environment'
        )
        choice(
            name: 'deployType',
            choices: ['regular update', 'restart from timestamp'],
            description: 'Deploy type'
        )
        string(
            name: 'parallelism',
            description: 'Parallelism values for each region (comma separated, e.g., 2,3)',
            trim: true
        )
        string(
            name: 'timestamp',
            description: 'Timestamp for restart (only applicable for restart deploy type)',
            trim: true
        )
    }

    stages {
        stage('Select Regions') {
            steps {
                script {
                    // Define environment regions map
                    def environmentRegions = [
                        'prod': ['eu-west-1', 'eu-central-1', 'us-east-1', 'us-east-2', 'us-west-2'],
                        'smoke': ['us-east-1', 'us-west-2'],
                        'staging': ['eu-west-1', 'eu-central-1', 'us-east-1', 'us-east-2', 'us-west-2'],
                        'perf': ['us-east-1']
                    ]

                    // Fetch regions based on selected environment
                    def selectedEnvironment = params.environment
                    def regions = environmentRegions[selectedEnvironment]

                    // Ask user to select regions dynamically
                    def userInput = input(
                        id: 'userInput', 
                        message: 'Select Regions', 
                        parameters: [
                            choice(
                                name: 'regions',
                                choices: regions.join('\n'),
                                description: 'Select regions'
                            )
                        ]
                    )

                    // Set the regions parameter
                    env.selectedRegions = userInput
                }
            }
        }

        stage('Initialize') {
            steps {
                script {
                    echo "Environment: ${params.environment}"
                    echo "Regions: ${env.selectedRegions}"
                    echo "Deploy Type: ${params.deployType}"
                    echo "Parallelism: ${params.parallelism}"
                    echo "Timestamp: ${params.timestamp}"
                }
            }
        }

        // Add more stages as required
    }
}
