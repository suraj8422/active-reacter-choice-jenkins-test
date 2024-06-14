/*
pipeline {
    agent any
    
    environment {
        // Placeholder for dynamically determined values
        SELECTED_REGIONS = ''
    }
    
    parameters {
        choice(name: 'environment', choices: ['staging', 'perf', 'smoke', 'prod'], description: 'Select the environment')
        choice(name: 'operation', choices: ['deploy', 'dry-run'], description: 'Select the operation')
        string(name: 'parallelism', description: 'Parallelism values (comma separated, e.g., 2,3)', trim: true)
        string(name: 'timestamp', description: 'Timestamp for restart (only applicable for restart deploy type)', trim: true)
    }

    stages {
        stage('User Input') {
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

                    // Collect dynamic regions input
                    def userInput = input(
                        id: 'userInput',
                        message: "Preparing to deploy to ${selectedEnvironment}",
                        parameters: [
                            choice(
                                name: 'regions',
                                choices: regions.join('\n'),
                                description: 'Select regions'
                            )
                        ]
                    )
                    env.SELECTED_REGIONS = userInput
                }
            }
        }

        stage('Summary and Warnings') {
            steps {
                script {
                    def summary = """
                    Summary of Inputs:
                    - Environment: ${params.environment}
                    - Operation: ${params.operation}
                    - Regions: ${env.SELECTED_REGIONS}
                    - Parallelism: ${params.parallelism}
                    - Timestamp: ${params.timestamp}
                    """
                    echo summary

                    if (params.environment == 'smoke' && params.operation == 'deploy') {
                        echo "Warning: Incompatible with smoke environment."
                    }
                }
            }
        }

        stage('Dry Run and Safeguards') {
            steps {
                script {
                    if (params.operation == 'dry-run') {
                        echo "Dry-run selected. Showing safeguards and warnings."
                        // Simulate checks and display any warnings
                    } else {
                        echo "Proceeding with deployment."
                    }
                }
            }
        }

        stage('Deploy') {
            when {
                expression { params.operation == 'deploy' }
            }
            steps {
                script {
                    echo "Deploying to environment: ${params.environment}"
                    echo "Regions: ${env.SELECTED_REGIONS}"
                    echo "Parallelism: ${params.parallelism}"
                    echo "Timestamp: ${params.timestamp}"
                    // Add deployment logic here
                }
            }
        }

        stage('Post-Execution') {
            steps {
                script {
                    // Add any post-execution logic, such as providing links for verification
                    echo "Execution complete. Check AWS processor for verification."
                }
            }
        }
    }
}
*/

properties([
    parameters([
        choice(
            choices: ['Gujarat', 'Maharashtra', 'Punjab'],
            description: 'Select State',
            name: 'state'
        ),
        activeChoiceReactiveParam(
            name: 'cities',
            description: 'Select City',
            filterable: false,
            choiceType: 'MULTI_SELECT',
            groovyScript: [
                classpath: [],
                script: '''
                    if (params.state == "Gujarat") {
                        return ["Rajkot", "Ahmedabad", "Jamnagar"]
                    } else if (params.state == "Maharashtra") {
                        return ["Mumbai", "Pune", "Nagpur"]
                    } else if (params.state == "Punjab") {
                        return ["Ludhiana", "Amritsar", "Jalandhar"]
                    } else {
                        return ["No match"]
                    }
                '''
            ]
        )
    ])
])

pipeline {
    agent any
    stages {
        stage('Display Parameters') {
            steps {
                script {
                    echo "Selected State: ${params.state}"
                    echo "Selected City: ${params.cities}"
                }
            }
        }
        // Add more stages as required
    }
}
