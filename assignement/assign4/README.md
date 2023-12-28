# Assignment 4

This guide will help you understand how to set up a MySQL container with persistent storage for both configuration and data.

## **Objective**

Demonstrate understanding of using bind mounts with MySQL for persistent data storage.

### **Steps:**

#### 1. Create Volume for Persistent MySQL Configuration

Create a directory on your host system to store MySQL configuration files persistently. This directory will be mounted to the MySQL container.

```bash
mkdir -p ~/mysql/config
```

#### 2. Create Volume for Persistent MySQL Data

Similarly, create another directory for MySQL data storage. This will ensure data persistence across container restarts.

```bash
mkdir -p ~/mysql/data
```

#### 3. Create MySQL Container with These Volumes in Use

Launch a MySQL container, using the created directories as bind mounts for configuration and data. Set the necessary environment variables like `MYSQL_ROOT_PASSWORD`.

```bash
docker run --name mysql_container -v ~/mysql/data:/var/lib/mysql -v ~/mysql/config:/etc/mysql/conf.d -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql:latest
```

In this command:

- `~/mysql/data:/var/lib/mysql` mounts the host directory for MySQL data inside the container.
- `~/mysql/config:/etc/mysql/conf.d` mounts the host directory for MySQL configuration.
- `MYSQL_ROOT_PASSWORD` is an environment variable used to set the root password for MySQL.

---

To test and verify that your MySQL container setup with bind mounts for persistent data storage is working correctly, you can follow these steps:

### Testing MySQL Container for Persistence

#### 1. Access the MySQL Container

First, access the MySQL container's command line interface. You'll need the root password that you set when creating the container (`my-secret-pw` in your example).

```bash
docker exec -it mysql_container mysql -uroot -p
```

#### 2. Create a Test Database and Table

Once inside the MySQL CLI, create a test database and table, then insert some data.

```sql
CREATE DATABASE test_db;
USE test_db;
CREATE TABLE test_table (id INT AUTO_INCREMENT, name VARCHAR(255), PRIMARY KEY(id));
INSERT INTO test_table (name) VALUES ('Test Data');
```

#### 3. Verify Data Insertion

Check if the data is inserted correctly.

```sql
SELECT * FROM test_table;
```

You should see the 'Test Data' entry.

#### 4. Exit MySQL and Stop the Container

Exit the MySQL command line and stop the container.

```bash
exit
docker stop mysql_container
```

#### 5. Restart the MySQL Container

Restart the container to check for data persistence.

```bash
docker start mysql_container
```

#### 6. Access the MySQL Container Again

Access the container and MySQL CLI as before.

```bash
docker exec -it mysql_container mysql -uroot -p
```

#### 7. Check for Persistent Data

Use the MySQL CLI to check if the test database and data are still there.

```sql
USE test_db;
SELECT * FROM test_table;
```

If you see the 'Test Data' entry, it means the data persisted across container restarts, demonstrating that your bind mounts are working correctly.

#### 8. Inspect the Mounted Host Directories

Optionally, you can also inspect the mounted directories on your host machine to see the MySQL files:

```bash
ls ~/mysql/data
ls ~/mysql/config
```

These directories should contain MySQL data and configuration files, respectively.

---

By following these steps, you can verify that your MySQL container is correctly using bind mounts for persistent data storage, ensuring that data remains intact across container restarts.

---

This assignment demonstrates the use of bind mounts in Docker for maintaining persistent data and configuration for a MySQL database. By mounting host directories to the container, any changes made to the database or configuration files inside the container are reflected and stored on the host machine, ensuring data persistence beyond the lifecycle of the container.

This `README.md` provides comprehensive instructions and code snippets for Assignment 4, focusing on using bind mounts with MySQL in Docker, and is formatted in markdown for immediate use.

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
