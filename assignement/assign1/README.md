# Assignment 1

Demonstrate a clear understanding of the basic concepts of Docker volumes.

## **Steps:**

1. Create a Docker volume and list it using the `docker volume ls` command.
2. Run a Docker container and attach the volume created in step one.
3. Inside the container, write a simple text file to the attached volume.
4. Remove the container created in step two, and create a new container and attach it to the same volume.
5. Verify the existence of the text file written in step three in the new container.

### 1. Create a Docker Volume and List It

To create a Docker volume, use the `docker volume create` command. Then, list all volumes using `docker volume ls`.

```bash
docker volume create my_volume
docker volume ls
```

### 2. Run a Docker Container and Attach the Volume

Run a Docker container (using `alpine` for simplicity) and attach the created volume to it. The volume will be mounted at `/data` in the container.

```bash
docker run -it --name my_container -v my_volume:/data alpine sh
```

### 3. Inside the Container, Write a Simple Text File to the Attached Volume

While inside the container, create a text file within the mounted volume.

```bash
echo "Hello from Docker!" > /data/hello.txt
exit
```

### 4. Remove the Container and Create a New One with the Same Volume

Remove the first container, then create a new one, attaching the same volume.

```bash
docker rm my_container
docker run -it --name new_container -v my_volume:/data alpine sh
```

### 5. Verify the Existence of the Text File in the New Container

Check the contents of the `/data` directory in the new container to verify the existence of the `hello.txt` file.

```bash
cat /data/hello.txt
```

You should see the output: `Hello from Docker!`, confirming that the file written in the previous container persists in the volume.

## Required Reading

- The first few paragraphs of [the docker documentation on volumes](https://docs.docker.com/storage/volumes/)
- The first few paragraphs of [the docker documentation on bind mounts](https://docs.docker.com/storage/bind-mounts/)
