<h1> Concourse </h1>

- [Software setups](#software-setups)
- [Steps](#steps)
  - [Initial Setup](#initial-setup)
  - [Hello World](#hello-world)
- [Reference](#reference)

# Software setups
1. [Docker](https://www.docker.com/community-edition)
2. [Docker Compose](https://docs.docker.com/compose/install/#install-compose) - Didn't install it

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
6. 





# Reference 
* https://concoursetutorial.com/
* https://github.com/starkandwayne/concourse-tutorial.git