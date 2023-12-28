# Introduction: Docker Bind Mounts

Bind mounts in Docker allow direct mapping of host system directories or files to container directories, enabling access to host resources, sharing of data, and persistent storage. They are very helpful during development and testing when there is a need to interact with or utilize host system files or directories from within containers.

## Lab

- Run the `nginx` container at the detached mod, name the container as `nginx-default`, and open in the browser and show the nginx default page.

```bash
docker run -d --name nginx-default -p 80:80  nginx
```

- Create a folder named webpage, and an index.html file.

```bash
mkdir webpage
cd webpage
echo "<h1>Hi Doctor Chandra:)</h1>" > index.html
```

- Run the `nginx` container at the detached mod, name the container as `nginx-docker-chandra`, attach the directory `/home/ec2-user/webpage` to `/usr/share/nginx/html` mount point in the container, and open on browser and show the web page.

```bash
docker run -d --name nginx-docker-chandra -p 80:80 -v /home/$USER/webpage:/usr/share/nginx/html nginx
```

## More ways to bind-mount the path

```bash
docker run -d -it --name devtest-mount --mount type=bind,source="$(pwd)"/vol-test,target=/app \
 nginx:latest

docker run -d -it --name devtest -v "$(pwd)"/vol-test:/app nginx:latest
```

## References

- [Docker documentation on bind mounts w/a good illustration.](https://docs.docker.com/storage/bind-mounts/). The documentation goes in-depth on various bind-mount use cases & has good example code. The first few paragraphs are a very useful overview / reference.

---
