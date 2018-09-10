Running an application as

	Final Output: Multi-branch pipeline intelligent enough to understand which branch or pull-request it's being run against and perform certain steps on basis of it (details below).


	Create a Git repository with two branches: 'integration' and 'master'. Have a Dockerfile and Jenkinsfile in the repository.

	1. When the pipeline is run against integration branch, create a Docker image using the Dockerfile available in repo.

	2. When the pipeline is run against a PR (which merges code from integration to master), create image, run it as container and, test the running container to validate if the container is doing what is supposed to do.

	3. When the pipeline is run against master, deploy the container to a Kubernetes instance as a deployment.
