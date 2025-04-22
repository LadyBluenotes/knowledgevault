Docker is an open-source project that can be used to create lightweight, portable self-sufficient containers from and for any application.

## Basics

Information from <https://docs.docker.com/get-started/docker-concepts/the-basics/>.

### Containers

*Isolated* processes for each of an applications components. Each component, such as the front-end, API engine, and the database, can run in its own isolated environment, completely isolated from everything else on your machine.

Containers are:
- *Self-contained*: has everything it needs to function with no need for any pre-installed dependencies on the host machine.
- *Isolated*: minimal influence on host and other containers, which increases the security of your applications.
- *Independent*: managed independently, meaning deleting one container will not affect others.
- *Portable*: since containers can run anywhere, the container running on one machine will work the same as anywhere else.

#### Versus Virtual Machines (VM)

Since a VM is an entire operating system, including its own kernel, hardware drivers, programs, and applications, spinning one up only to isolate an application can create a lot of overhead.

Containers being an isolated process with all the files that it needs to run, allow you to run more applications on less infrastructure.

Containers and VMs can be used together. This means that instead of provisioning one machine to run a single application, a VM can run with a container runtime can run multiple containerized applications, increasing the resource utilization and reducing costs.

### Images

Container images are standardized packages that include all files, binaries, libraries, and configurations to run a container.

There are two important principles of images:
1. *Immutability* - Once an image is created, it cannot be modified. You can make changes on top of it or create a new one.
2. *Layer composition* - Each layer represents a set of file system changes that add, remove, or modify files.

These two principles let you extend or add to existing images. For example, you can start from one image (eg. Python) and add additional layers to install your application's dependencies and add to your code which creates focus on the app rather than original image itself.

### Registry

Image registry is a centralized location for storing and sharing container images. Can be either *public* or *private*. [Docker Hub](#docker-hub) is a *public* registry that anyone can use and is the *default*.

Other available container registries include:
- [Amazon Elastic Container Registry (ECR)](https://aws.amazon.com/ecr/)
- [Azure Container Registry (ACR)](https://azure.microsoft.com/en-in/products/container-registry)
- [Google Container Registry (GCR)](https://cloud.google.com/artifact-registry)

*Private* registries can be run on your own local system or within your organization.

#### Versus Repository

A **registry** is a centralized location that stores and manages *container images* whereas a **repository** is a collection of related container images *within* a registry. In other words, a repository is a folder where you organize your images based on *projects* and each repository has one or more container images.

## Images

### Image Layers

Each layer of an image is *immutable*. They contain a set of filesystem changes (additions, deletions, modifications) and can let you extend images of others by reusing their base layers and allowing you to add only the data that your application needs.

An example image:
1. First layer adds basic commands and a package manager.
2. Second layer installs a runtime and something for dependency management.
3. Third layer copies in an application's specific requirements file.
4. Fourth layer installs application-specific dependencies.
5. Fifth layer copies in actual source code for application.

This layer allows them to be reused between images. For example, if you wanted to use another application with the same runtime, it can leverage the same base. This improves the build times and reduces storage and bandwidth required to distribute the image.

#### Stacking Layers

Layering is made possible through content-addressable storage and union file systems.

1. After each layer is downloaded, it is extracted into its *own directory* on the host filesystem.
2. When a container is run from an image, a *union filesystem* is created where layers are stacked on top of each other, creating a new and unified view.
3. When a container starts, its root is set to the location of this *unified directory*, using `chroot`.

Once the union filesystem is created, in addition to image layers, a directory is created *specifically* for the running container. This lets the container make filesystem changes, while also letting the original image. Therefore, multiple containers can be run from the same underlying image.

### Building Images

Most often, built using a [Dockerfile](#dockerfile). When running a build, the builder pulls the base image (if needed), then runs the instructions set forth in the Dockerfile.

Most basic `docker build` command would look like `docker build .` where the `.` provides the path or URL to the build context, where the Dockerfile and other referenced files are. With this command, the image won't have a name, but will output the ID of the image.

```shell
docker build .
[+] Building 3.5s (11/11) FINISHED                                              docker:desktop-linux
 => [internal] load build definition from Dockerfile                                            0.0s
 => => transferring dockerfile: 308B                                                            0.0s
 => [internal] load metadata for docker.io/library/python:3.12                                  0.0s
 => [internal] load .dockerignore                                                               0.0s
 => => transferring context: 2B                                                                 0.0s
 => [1/6] FROM docker.io/library/python:3.12                                                    0.0s
 => [internal] load build context                                                               0.0s
 => => transferring context: 123B                                                               0.0s
 => [2/6] WORKDIR /usr/local/app                                                                0.0s
 => [3/6] RUN useradd app                                                                       0.1s
 => [4/6] COPY ./requirements.txt ./requirements.txt                                            0.0s
 => [5/6] RUN pip install --no-cache-dir --upgrade -r requirements.txt                          3.2s
 => [6/6] COPY ./app ./app                                                                      0.0s
 => exporting to image                                                                          0.1s
 => => exporting layers                                                                         0.1s
 => => writing image sha256:9924dfd9350407b3df01d1a0e1033b1e543523ce7d5d5e2c83a724480ebe8f00    0.0s
```

You can start a container by using the referenced image. The names are typically not memorable, which is why [tagging images](#tagging-images) is useful.

```shell
docker run sha256:9924dfd9350407b3df01d1a0e1033b1e543523ce7d5d5e2c83a724480ebe8f00
```

### Tagging Images

Method to provide an image with a *memorable name*. The structure to nam eof an image is:

```text
[HOST[:PORT_NUMBER]/]PATH[:TAG]
```

- `HOST`: optional registry hostname where image is located. If not specified, `docker.io` (Docker's public registry) is used by default.
- `PORT_NUMBER`: registry port number if a hostname is provided
- `PATH`: path of image. Consist of slash-separated components.
	- For Docker Hub - `[NAMESPACE/]REPOSITORY` where namespace is user or org name. If no namespace, `library` (Docker Official Images) is used.
- `TAG`: Custom, human-readable identifier typically used to identify different versions or variants of an image. `latest` is used by default.

### Publishing Images

Once an image has been built and tagged and is now ready for the registry, use the `docker push` command.

```shell
docker push my-username/my-image
```

Within some time, all layers for the image will be pushed to the registry.

> Before an image is able to be pushed to a repo, authentication is needed. Use the `docker login` command to do so.

### Build Cache

For each instruction within the Dockerfile, Docker checks whether it can *reuse* the instruction from the previous build. If a similar instruction has been executed previously, Docker will not redo it and, instead, will use the cached result. This improves the time of the build processes making them more efficient and saving valuable time and resources.

Examples of cache invalidation:
- Any changes to the command of a `RUN` instruction. Docker detects the change and invalidates the build cache.
- Any changes to files copied into the image with `COPY` or `ADD`. Any alterations within the project directory, whether content or properties like permissions, Docker considers these modifications as triggers to invalidate the cache.
- Once a single layer is invalidated, all following ones are as well. If a previous layer, including base or intermediary layers, have been invalidated due to changes, Docker will ensure any subsequent ones are also invalidated. This keeps the build process synchronized and prevents inconsistencies.

### Multi-stage Builds

In traditional builds, all instructions are executed in sequence, and in a single build container: downloading dependencies, compiling code, and packaging the application. All these layers lead up to final image, but can create bulky images that carry unnecessary weight and increase security risks.

Multi-stage builds introduce multiple stages to your Dockerfile, each with a specific purpose. This creates the ability to run different parts of a build in different environments, concurrently. Through separating the build environment from final runtime environment, image size and attack surface are reduced. This is helpful for applications with large build dependencies.

Multi-stage builds are recommended for all types of applications.

- For interpreted languages (eg. JavaScript, Ruby, Python), the code can be built and minified in one stage, the production-ready files can be copied to a smaller runtime image. This optimizes image for deployment.
- For compiled languages (eg. C, Go, Rust), multi-stage builds let you compile in one stage and copy compiled binaries into a final runtime image. No bundle needed for entire compiler in final image.

## Dockerfile

A text-based document used to *create* a container image. Provides instruction to image builder on what commands to run, files to copy, startup commands, etc.

For more information: <https://docs.docker.com/reference/dockerfile/>

### Common Instructions

| Instruction                     | What it does                                                                                  |
| ------------------------------- | --------------------------------------------------------------------------------------------- |
| `FROM <image>`                  | Specifies base image that build will extend                                                   |
| `WORKDIR <path>`                | Specifies working directory or path in image where files will be copied and commands executed |
| `COPY <host-path> <image-path>` | Tells builder to copy files from host and put them into container image                       |
| `RUN <command>`                 | Tells builder to run specified command                                                        |
| `ENV <name> <value>`            | Sets environment variable that running container will use                                     |
| `EXPOSE <port-value>`           | Sets config on image that indicates a port image would like to expose                         |
| `USER <user-or-uid>`            | Sets default user for all subsequent instructions                                             |
| `CMD ["<command>", "<arg1>"`    | Sets default command a container using this image will run                                    |

## Docker Desktop

All-in-one package that helps you helps you build images, run containers, and more. This simplifies the container management by streamlining setup, config, and compatibility across different environments. This can be helpful by removing the pain points of environment inconsistencies and deployment challenges.

- **Exec Tab**: will see information about your container, including logs and files. Can even the shell by selecting this tab.
- **Inspect tab**: detailed information about your container. This will perform various actions such as pause, resume, start, or stopping containers. Can also explore **Logs**, **Bind mounts**, **Files**, and **Stats** tabs.

## Docker Hub

Global marketplace for storing and distributing images. Provides a variety of Docker-supported and *endorsed* images known as **Docker Trusted Content**. These provide fully managed services or starters for your own images, including:
- [Official Docker Images](https://hub.docker.com/search?q=&type=image&image_filter=official): curated and serve as the starting point for many users. Contain some of the most secure on Docker Hub.
- [Verfifed Publishers](https://hub.docker.com/search?q=&image_filter=store): high-quality images from commercial publishers
- [Docker-Sponsored OSS](https://hub.docker.com/search?q=&image_filter=open_source): images published and maintained by OSS projects, sponsored by Docker through Docker's OSS program.

## Docker Compose

While the `docker run` commands can be used to start multiple containers, but managing and cleaning them up can be difficult. For example, you need to manage networks, flags needed to connect containers to those networks, and then cleanup them up which is also complicated.

Docker Compose helps you define all containers and their configurations within a single YAML file. If this is within the code repo, anyone that clones said repo can be up and running with a single command.

Compose is a **declarative** tool, you just need to define it then go. Not everything needs to be recreated from scratch. To make a change, running `docker compose up` will reconcile changes in your file and apply them intelligently.

> A Dockerfile provides instructions to build a container while a Compose file defines your running containers.
> Compose files often *reference* a Dockerfile to build an image to use for a particular service.