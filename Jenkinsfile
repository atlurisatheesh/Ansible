pipeline {
    agent any
    environment {                                  // Pipeline Variables : All the stages of the pipeline can use it.
        
        SSH_CRED = credentials('SSH_CRED')
    }

     parameters {
        string(name: 'PERSON', defaultValue: 'redis', description: 'Please enter your value') 
        choice(name: 'CHOICE', choices: ['dev', 'prod', 'stage'], description: 'Select one of the environment')
        
    }

    stages {

        // stage('Lint Checks') {                     // This stage will only be executed when you run the job from a feature branch
        //     // when { branch pattern: "feature/.*", comparator: "REGEXP"}
        //     steps {
        //         sh '''
        //             env 
        //             echo **** Starting Lint Checks ****
        //             echo **** Lint Checks Completed ****
        //         '''
        //     }
        // }

         stage('Performing a dry run') {                     // This stage should only run when you raise a PULL Request.
            // when { branch pattern: "PR-.*", comparator: "REGEXP"}
            steps {
                sh '''
                    env 
                    ansible-playbook robo-dryrun.yml  -e ENV=dev -e COMPONENT=redis -e ansible_user=${SSH_CRED_USR} -e ansible_password=${SSH_CRED_PSW} 
                '''
            }
        }
    }
}