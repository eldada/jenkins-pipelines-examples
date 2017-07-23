# Jenkins Pipelines Examples
Keep a few examples of Jenkins Pipelines. Mostly used for demo and training.

Look in each directory and find the `Jenkinsfile` with the example. See more details are in the `Jenkinsfile` comments.

**You are more than welcome to contribute, share and ask.**

## Setup Local Jenkins
These examples assume a simple setup of a single Jenkins master and two agents.

The setup is installed and run in a [Vagrant](https://www.vagrantup.com/) image.

### Spin up the Vagrant VM
Run the following in the root of the repository
```bash
# Spin up the Vagrant VM
$ vagrant up

# Once finished, ssh into VM
$ vagrant ssh
```

### Start a local Jenkins master
- Build the custom Jenkins Docker image
```bash
# Go into the directory that has the repository files
$ cd /opt/provisioning/

# Build the Jenkins Docker image
$ docker build -t jenkinsx:1 -f jenkins/Dockerfile .
```

- Prepare directories and permissions
```bash
# Permissions on /var/run/docker.sock
$ sudo chmod 666 /var/run/docker.sock

# Directory for Jenkins home
$ mkdir -p ~/jenkins_home
$ chmod -R 777 ~/jenkins_home
```

- Start the Jenkins master
```bash
$ docker run -d --name jenkins -p 8080:8080 -p 50000:50000 -v /var/run/docker.sock:/var/run/docker.sock -v ~/jenkins_home:/var/jenkins_home jenkinsx:1
```
- Browse to http://192.168.17.17:8080 and complete the initial setup wizard
  - Get initial admin password from `docker logs jenkins` output
  - Install suggested plugins
  - Install the **Docker Slaves Plugin** (for dynamic Docker agent provisioning per build)
  - Install the **Blue Ocean plugin** (recommended)
- Define two Jenkins agents (slaves)
  - Create two nodes from the `Manage Jenkins` -> `Manage Nodes`
  - Call the nodes `agent1` and `agent2`
  - Set remote root directory to `/home/jenkins`
  - Configure them to `Launch method` -> `Launch agent via Java Web Start`
  - Get the secret token for each node (**AGENT1_TOKEN** and **AGENT2_TOKEN**)

### Start two Jenkins agents (slaves)
Once you have the tokens for the agents, start the two agents
```bash
# Start agent 1
$ docker run -d --link jenkins:jenkins-server --name agent1 jenkinsci/jnlp-slave:3.7-1 -url http://jenkins-server:8080 ${AGENT1_TOKEN} agent1

# Start agent 2
$ docker run -d --link jenkins:jenkins-server --name agent2 jenkinsci/jnlp-slave:3.7-1 -url http://jenkins-server:8080 ${AGENT2_TOKEN} agent2

```

### Create Pipeline jobs
You can create a Pipeline type job using any of the provided examples in the different directories
