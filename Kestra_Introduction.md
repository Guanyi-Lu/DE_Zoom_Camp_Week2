## Workflow Orchestration

### What is an Orchestrator:
<https://kestra.io/blogs/2024-09-18-what-is-an-orchestrator>


### Three key properties within each flow:
In Kestra platform, workflows known as Flows, it's declared in YAML, it works wih any language
1. id: name of your flow
2. namespace:environment for your flow (test/prod)
3. tasks:  list of tasks to execute in your flow

input,output,triggers
### Kestra installation
#### Download the docker image:
The below command starts Kestra with an embedded H2 database that will not persist data
```bash
docker run --pull=always --rm -it -p 8080:8080 --user=root -v /var/run/docker.sock:/var/run/docker.sock -v /tmp:/tmp kestra/kestra:latest server local
```
#### Docker compose installation
Download the Docker Compose file using the following command on Linux and macOS
```bash
curl -o docker-compose.yml \
https://raw.githubusercontent.com/kestra-io/kestra/develop/docker-compose.yml
```
#### hello_world documentation:
1. initial localhost:8080 to log in to kestra UI
2. Files in the Kestra UI(namespace:company.team):

api_examples.py:
```python
import requests

r=requests.get("https://api.github.com/repos/kestra-io/kestra")
gh_stars=r.json()['stargazers_count']
print(gh_stars)
```
##### Function
To interact with the GitHub API and fetch the number of stars for the Kestra repository.

requirements.txt:
requests
##### Function
This file lists all the external Python dependencies (i.e., libraries or packages) that need to be installed in your environment. It ensures that anyone working on the project can set up the same environment with the same versions of dependencies

Kestra flow:
```yaml
id: hello-world
namespace: company.team

tasks:
  - id: python_script
    type: io.kestra.plugin.scripts.python.Commands
    namespaceFiles:
      enabled: true
    beforeCommands:
      - python3 -m venv .venv  # Create virtual environment (no need for a local path)
      - . .venv/bin/activate  # Activate virtual environment (Unix/Linux)
      - pip install -r company.team/scripts/requirements.txt  # Install dependencies
    commands:
      - python company.team/scripts/api_example.py  # Run Python script
    runner: PROCESS
```
##### Function
 The flow includes a task that runs a Python script (api_example.py) in a virtual environment. It sets up the environment, installs dependencies, and then executes the script.



## ETL: Extract data and load it to Postgres

docker-compose.yml file


## ETL: Extract data and load it to Google Cloud
gcp_taxi_scheduled.yaml file

## Scheduling and Backfills
see description in gcp_taxi_scheduled.yaml file

## Install Kestra on the Cloud and sync your Flows with Git
see https://kestra.io/docs/installation/gcp-vm
