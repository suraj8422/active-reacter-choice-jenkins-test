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
