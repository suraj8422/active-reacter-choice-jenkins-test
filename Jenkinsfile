// Define parallelism values
def parallelismValues = [
    prod: [ 'eu-west-1': 16, 'eu-central-1': 16, 'us-east-1': 16, 'us-east-2': 16, 'us-west-2': 16 ],
    smoke: [ 'us-east-1': 2, 'us-west-2': 8 ],
    staging: [ 'eu-west-1': 2, 'eu-central-1': 2, 'us-east-1': 2, 'us-east-2': 2, 'us-west-2': 2 ],
    perf: [ 'us-east-1': 4 ]
]

// Define environments
def envs = parallelismValues.keySet()

// Fetch regions dynamically based on selected environment
def selectedEnv = params.environment
def regions = parallelismValues[selectedEnv]?.keySet()?.join(',')

// Define pipeline properties with dynamic parameters
properties([
    parameters([
        choice(
            choices: envs.join('\n'), 
            description: 'Select environment', 
            name: 'environment'
        ),
        string(
            description: 'Regions (comma separated)', 
            name: 'regions', 
            defaultValue: regions ?: '', 
            trim: true
        ),
        choice(
            choices: ['regular update', 'restart from timestamp'], 
            description: 'Deploy type', 
            name: 'deployType'
        ),
        string(
            description: 'Parallelism values for each region (comma separated, e.g., 2,3)', 
            name: 'parallelism', 
            trim: true
        ),
        string(
            description: 'Timestamp for restart (only applicable for restart deploy type)', 
            name: 'timestamp', 
            trim: true
        )
    ])
])

pipeline {
    agent any
    stages {
        stage('Fetch User Input') {
            steps {
                script {
                    // Fetch user input
                    def selectedEnvironment = params.environment
                    def selectedRegions = params.regions.split(',').collect { it.trim() }
                    def deployType = params.deployType
                    def parallelism = params.parallelism.split(',').collect { it.trim().toInteger() }
                    def timestamp = params.timestamp

                    echo "Selected Environment: ${selectedEnvironment}"
                    echo "Selected Regions: ${selectedRegions}"
                    echo "Deploy Type: ${deployType}"
                    echo "Parallelism: ${parallelism}"
                    echo "Timestamp: ${timestamp}"

                    // Use the fetched values as needed in subsequent steps
                    // Example: Set environment variables or perform conditional logic
                }
            }
        }

        // Add more stages as needed for your pipeline
    }
}
