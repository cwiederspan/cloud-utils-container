# Cloud Utility Container

Creates a Docker container containing several cloud-related utilities. By using a container for these utilities, it eliminates
the need to install and version these utilities natively on the local machine.

## Included Utilities

* [Git](https://git-scm.com/)
* [Node/NPM](https://node.js)
* [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/?view=azure-cli-latest)
* [Terraform](https://www.terraform.io/)
* [Kubectl](https://kubernetes.io/docs/reference/kubectl/overview/)
* [Helm](https://helm.sh/)
<!-- * [Dapr](https://dapr.io/) -->

## Background

I have been a developer for a long time, and I am always looking for ways to be more efficient. One of the things I have grown
to hate is the process of reformatting and setting up my primary developer machine. As a full-stack developer, this requires me
to install a bunch of GUI tools such as VS Code, Visual Studio, SQL Management Studio, etc. This part is not terrible because
I can simply download and install from the web and I will get the latest versions and continuous updates.

However, there has been a huge shift in the way I do a lot of my development with the advent of Docker, .NET Core and WSL 2.
I am doing more and more command line stuff with utilities such as the Git, Azure CLI and Terraform to name just a few. The
problem with this is that these tools take, at least for me, much more energy to install and upkeep. I have to remember whether
they can be setup with apt get, or perhaps they are just a simple binary that I need to get into the PATH.

So, with a brand new Surface Laptop 3 in-hand, I am going to take a different approach and containerize all of those utilities
into a single Docker container, and then use that with a combination of [Remote WSL Development](https://code.visualstudio.com/docs/remote/wsl)
that is now part of VS Code.

## Approach

The approach is simple - I just need a container image that has all of our utilities setup and available. To accomplish this,
I need to stitch together a monster [Dockerfile](./Dockerfile) that gets everything into the image. I used several examples, like
[this](https://github.com/microsoft/vscode-dev-containers/blob/master/containers/azure-cli/.devcontainer/Dockerfile),
[this](https://github.com/microsoft/vscode-dev-containers/blob/master/containers/azure-terraform/.devcontainer/Dockerfile) and
[this](https://helm.sh/docs/intro/install/) to help guide me.

> **DISCLAIMER:** This Dockerfile goes way beyond the typical .NET Core version that I normally get for free from Visual Studio,
> so I make no claims that it is ideal or efficient. So far, it is working for my needs and it will continue to evolve over as
> I add additional utilities and update versions.

There also a [docker-compose.yaml](./docker-compose.yml) that I use to make building and running the container easier. I also
use this file to mount my local code directory (C:\Projects) to the container so everything is accessible from inside the
running container.

> **NOTE:** Update the docker-compose.yml file with any necessary changes to the path, or desired image or container names.

This is everything I need to build and run the container on my laptop:

```bash
docker-compose up -d --build
```

## Getting Started

Now that the container is running, you can `exec` into it to begin working.

```bash
docker exec -it cloud_utils bash
```
