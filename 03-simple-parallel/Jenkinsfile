#!/usr/bin/env groovy

// A simple example of running parallel tasks on master and slaves

node ('master'){
    stage ('Init work on master'){
        echo "Initial work done on master"
        sh 'echo Time is: $(date)'
    }

    stage ('Parallel builds')
    parallel (
        "Thread 1" : {
            node ('master'){
                echo 'Running on master'
                sh 'echo ---------------; echo Hostname is $(hostname); echo Time is $(date); sleep 5; touch file.master'
            }
        },
        "Thread 2" : {
            node ('agent1'){
                echo 'Running on agent1'
                sh 'echo ---------------; echo Hostname is $(hostname); echo Time is $(date); sleep 5; touch file.agent1'
            }
        },
        "Thread 3" : {
            node ('agent2'){
                echo 'Running on agent2'
                sh 'echo ---------------; echo Hostname is $(hostname); echo Time is $(date); sleep 5; touch file.agent2'
            }
        }
    )

    stage ('Closeup on master'){
        echo "Finish work done on master"
        sh 'echo Time is: $(date)'
    }

}
