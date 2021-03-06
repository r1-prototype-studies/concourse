<h1> Concourse </h1>

- [Software setups](#software-setups)
- [Visual studio code extensions:](#visual-studio-code-extensions)
- [Steps](#steps)
  - [Initial Setup](#initial-setup)
  - [Hello World](#hello-world)
  - [Pipelines](#pipelines)
  - [Jobs](#jobs)
- [Troubleshooting](#troubleshooting)
- [Reference](#reference)

# Software setups
1. [Docker](https://www.docker.com/community-edition)
2. [Docker Compose](https://docs.docker.com/compose/install/#install-compose) - Didn't install it

# Visual studio code extensions:
1. Concourse CI Pipeline Editor
   
# Steps
## Initial Setup
1. Install the softwares
2. Create a new file  docker-compose.yml with the contents from https://raw.githubusercontent.com/starkandwayne/concourse-tutorial/master/docker-compose.yml
3. Open cmd and navigate to the file created path
4. Execute the below command
    ```cmd
    docker-compose up -d
5. Concourse will open in http://localhost:8080/
6. Download fly and add the file path to path environment variable
7. Setup concourse target using the below command
   ```cmd
   fly --target tutorial login --concourse-url http://127.0.0.1:8080 -u admin -p admin
8. Sync the fly version using the below command
    ```cmd
    fly --target tutorial sync
9. Saved target list can be seen using the below command
    ```
    cat ~/.flyrc
    ```
    
## Hello World
1. Create the yml file for the task
2. Use [] to send arguments to echo
3. Execute the below cmd to run the task
    ```
    fly -t tutorial execute -c task_helloWorld.yml
4. Builds can be seen in http://127.0.0.1:8080/builds/1
5. ``` 
    fly -t tutorial execute -c task_noInputs.yml 
6. Add -i and then the name of the input parameter for passing parameters
    ```
    fly -t tutorial e -c .\task_inputsRequired.yml -i some-important-input=.

    fly -t tutorial e -c .\task_inputsRequired.yml -i some-important-input=./testFolder

    fly -t tutorial e -c .\task_inputParentDir.yml
    ```
## Pipelines
1. Command to set the pipeline with the pipeline name
    ```
    fly -t tutorial sp -c pipeline_helloWorld.yml -p first_pipeline
2. unpause the task in the pipeline with the pipeline name
    ```
    fly -t tutorial up -p first_pipeline
3. For every change in the pipeline, set-pipeline cmd should be executed
4. Resources should be defined at the top
5. Resources have the below
    * name --> Identifier
    * type --> type of the resource
    * source --> source for that resource
6. Jobs should have
    * name --> name of the job
    * plan --> has the sequence of steps that needs to be executed
7. Execute the below command to view the output of a job
    ```
    fly -t tutorial watch -j GITResource_pipeline/job-git-pipeline
8. See the output of a particular build
    ```
    fly -t tutorial watch -j GITResource_pipeline/job-git-pipeline --build 2
9. Get all the builds
    ```
    fly -t tutorial builds
10. Destroy the pipeline
    ```
    fly -t tutorial dp -p temp_pipeline
    ```

## Jobs
1. Job can be triggered using the below command
    ```
    fly -t tutorial trigger-job -j first_pipeline/job-hello-world
2. Trigger job along with watch
    ```
    fly -t tutorial trigger-job -j GITResource_pipeline/job-git-pipeline -w
3. trigger: true can be set to the job
4. time resource can be used to trigger the job on a time basis
5. 


# Troubleshooting
1. Check the formatting in the Yaml file for the below error
    >error converting YAML to JSON: yaml: line 11: mapping values are not allowed in this context</>
    
    Check whether there is space after "-" in the yml file. 
2. Issue with shell script path
    >Backend error: Exit status: 500, message: {"Type":"","Message":"runc exec: exit status 1: exec failed: container_linux.go:345: starting container process caused \"exec: \\\"resource-tutorial/buildScripts/taskScripts/task_runTests.sh\\\": permission denied\"\n","Handle":"","ProcessID":"","Binary":""} 

    Change the scripts execution path as mentioned like here 
    Refer: https://github.com/concourse/concourse/issues/2161
3. 



# Reference 
* https://concoursetutorial.com/
* https://github.com/starkandwayne/concourse-tutorial.git
* https://hub.docker.com/
* 