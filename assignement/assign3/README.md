# Assignment 3

## **Objective**

Demonstrate understanding of bind mounts and how they can be used for data persistence.

This guide will walk you through the process of cloning a GitHub repository, modifying files within a Docker container, and observing the persistence of these changes on the host system.

### **Steps:**

#### 1. Create a Local Directory and Clone the Dojo-Jump Game

First, create a local directory and clone the `dojo-jump` game from the provided GitHub repository.

```bash
mkdir dojo-jump
cd dojo-jump
git clone https://github.com/chandradeoarya/dojo-jump.git .
```

#### 2. Start a Docker Container, Mounting the Local Directory

Start a Docker container (using `ubuntu` for ease of editing files), mounting the local `dojo-jump` directory. This will create a bind mount.

```bash
docker run -itd --name dojo_container -v $(pwd):/dojo-jump ubuntu
```

#### 3. Inside the Container, Modify the Game `index.html` File and Create a New File

Access the container, then modify the `index.html` file and create a new file in the `dojo-jump` directory.

```bash
docker exec -it dojo_container bash
cd /dojo-jump
echo "Modified content" >> index.html
echo "New content" > newfile.txt
exit
```

#### 4. Stop the Docker Container

Stop the container after making the modifications.

```bash
docker stop dojo_container
```

#### 5. Inspect the Changes Made to the Local Directory from the Host System

Finally, inspect the local directory to verify the changes made inside the container.

```bash
cat dojo-jump/index.html
cat dojo-jump/newfile.txt
```

You should see the modifications made to `index.html` and the content of the newly created `newfile.txt`. This demonstrates that changes made inside the container are reflected in the bind-mounted host directory.

---

This assignment illustrates the use of bind mounts in Docker for data persistence. It demonstrates how changes made inside a container to files in a bind-mounted directory are persistent and accessible from the host system, even after the container is stopped.

## Required Reading

- The first few paragraphs of [the docker documentation on volumes](https://docs.docker.com/storage/volumes/)
- The first few paragraphs of [the docker documentation on bind mounts](https://docs.docker.com/storage/bind-mounts/)

## Stretch assignment

Work through (read, run, and understand) the examples given in the above required readings. Start with the Docker Volumes documentation. Note that this will get into some topics (docker compose) we have not yet covered. Skip the examples which get very specific for particular technologies (such as the "selinux" and "CIFS/Samba volumes" sections). Skip "Bind propagation" except as background reading. Skip the part on "Block Device Storage" unless you really want to delve into it.

- You can mount EFS in Docker container volume to achieve remote storage mounting.

## Docker volume project

In this project you have to build and run todo-list flask app demonstrating using docker volume and bind mounting.

- Bind mount the source code the flask app container. You can use python3 image as the base image.
- Create mysql container with data and configuration persistance.
- Connect flask to use mysql database from the mysql container.
- Demonstrate the final working app.

**Note**: Can you think of some easier way to do this. Learn about Dockerfile. We will be using Dockerfile to create custom image for flask app backend.
