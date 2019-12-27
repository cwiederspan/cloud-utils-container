# Cloud Utility Container

Creates a Docker container containing several cloud-related utilties. By using a container for these utilities, it eliminates
the need to install and version these utilities natively on the local machine.

## Included Utilties

* [Git](https://git-scm.com/)
* [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/?view=azure-cli-latest)
* [Terraform](https://www.terraform.io/)
* [Kubectl](https://kubernetes.io/docs/reference/kubectl/overview/)
* [Helm](https://helm.sh/)

## Getting Started

> NOTE:  Update the docker-compose.yml file with any necessary changes to the path, or desired image or container names.

Use docker-compose to build the image, and then run it as a container locally. 

```bash
docker-compose up -d --build
```

Now that the container is running, you can `exec` into it to begin working.

```bash
docker exec -it cloud_utils bash
```