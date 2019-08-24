# Docker Container

Let try to pull the `busybox` image, run the container by executing shell command in one shot:

```bash
docker run -it busybox sh
```

This `docker run` format can be broken down into two parts:

1. docker run [options]
2. [image] [command]

- **options** `-it` means we want to Keep STDIN open even if not attached and allocate a pseudo-TTY.
- **image** we are using container busybox image.
- **command** running the sh command

To verify the container is running, type the following command from the new terminal:

```bash
docker ps
```

And you will see a similar response like this:

```
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
30b97ee57158        busybox             "sh"                7 seconds ago       Up 6 seconds                            charming_jones
```

Go back to the previous terminal and exit shell environment by running:

```bash
exit
```

Now verify the container again, you will see no container is currently running now:

```bash
docker ps
```
