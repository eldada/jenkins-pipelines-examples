# Jenkins Pipelines Examples
Keep a few examples of Jenkins Pipelines. Mostly used for demo and training.

## Setup Local Jenkins
These examples assume a simple setup of a single Jenkins master and two agents.

### Start a local Jenkins master
- Start a Jnekins master
```bash
$ docker run -d --name jenkins -p 8080:8080 -p 50000:50000 -v ~/.jenkins_home:/var/jenkins_home jenkins:2.60.1
```
- Browse to http://localhost:8080 and complete the initial setup wizard
- Create two nodes from the `Manage Jenkins` -> `Manage Nodes`
  - Call the nodes `agent1` and `agent2`
  - Configure them to `Launch method` -> `Launch agent via Java Web Start`
  - Get the secret token for each node (AGENT1_TOKEN and AGENT2_TOKEN)

### Start two Jenkins agents (slaves)
Once you have the tokens for the agents, start the two agents
```bash
$ docker run -d --link jenkins:jenkins-server --name agent1 jenkinsci/jnlp-slave:3.7-1 -url http://jenkins-server:8080 ${AGENT1_TOKEN} agent1

$ docker run -d --link jenkins:jenkins-server --name agent2 jenkinsci/jnlp-slave:3.7-1 -url http://jenkins-server:8080 ${AGENT2_TOKEN} agent2

```

### Create Pipeline jobs
You can create a Pipeline type job using any of the provided examples in the different directories
