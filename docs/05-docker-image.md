# Docker Image

To show all the images in the local machine

```bash
docker images
```

We will see the image `hello-world` since we have executed the `docker run` command and docker daemon pull it from docker hub for us before.

```
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
hello-world         latest              fce289e99eb9        7 months ago        1.84kB
```

Now let try to pull base image `busybox` via docker hub.

```bash
docker pull busybox
```

> if we didn't specify the tag, by default it will pull the latest tag.

Let review the images again:

```bash
docker images
```

You will see the new busybox image exist from the list:

```bash
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
busybox             latest              db8ee88ad75f        5 weeks ago         1.22MB
hello-world         latest              fce289e99eb9        7 months ago        1.84kB
```

Now, try to clean up and remove all images:

```bash
docker rmi db8ee88ad75f fce289e99eb9
```

Review the images again:

```bash
docker images
```

Now no image exists in the local machine:

```
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
```

Next: [Docker Container](06-docker-container.md)
