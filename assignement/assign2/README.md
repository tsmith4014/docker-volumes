# Assignment 2

## **Objective:**

Demonstrate an understanding of how to share Docker volumes between containers.

### **Steps:**

#### 1. Create a Docker Volume

First, create a new Docker volume. This volume will be shared between two containers.

```bash
docker volume create shared_volume
```

#### 2. Start Two Containers with the Created Volume Attached

Launch two separate containers (using `busybox` for simplicity), each with the shared volume mounted. We'll mount the volume at `/data` in both containers.

```bash
docker run -itd --name container1 -v shared_volume:/data busybox
docker run -itd --name container2 -v shared_volume:/data busybox
```

#### 3. In One Container, Create a Simple Text File

Access the first container and create a text file in the shared volume.

```bash
docker exec -it container1 sh
echo "Shared content" > /data/shared_file.txt
exit
```

#### 4. In the Other Container, Verify the Existence of the File

Access the second container and verify that the file created in the first container exists.

```bash
docker exec -it container2 sh
cat /data/shared_file.txt
exit
```

You should see the output: `Shared content`, confirming that the file is shared between the two containers.

#### 5. Edit the File and Show the Effect in Both Containers

Go back to the first container, edit the file, and then verify the changes from the second container.

```bash
# Edit in container1
docker exec -it container1 sh
echo "Updated content" >> /data/shared_file.txt
exit

# Verify in container2
docker exec -it container2 sh
cat /data/shared_file.txt
exit
```

The output in container2 should now include `Updated content`, demonstrating that changes made to the file in one container are immediately reflected in the other container.

This assignment shows how Docker volumes can be used to share data between containers in real-time. It demonstrates that any changes made to the volume's contents from one container are immediately visible to other containers that have the same volume mounted.

## Required Reading

- The first few paragraphs of [the docker documentation on volumes](https://docs.docker.com/storage/volumes/)
- The first few paragraphs of [the docker documentation on bind mounts](https://docs.docker.com/storage/bind-mounts/)
