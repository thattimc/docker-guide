# Docker Container

Let try to pull the `busybox` image, run the container by executing shell command in one shot:

```bash
docker run -it busybox sh
```

This `docker run` format can be broken down into two parts:

1. docker run [options]
2. [image] [command]

- **options** `-it` means we want to keep STDIN open even if not attached and allocate a pseudo-TTY
- **image** we are using container busybox image
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

Instead, the container still exists with the `Exited` status; you can verify it  by running:

```bash
docker ps -a
```

It will show a similar result:

```
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                     PORTS               NAMES
30b97ee57158        busybox             "sh"                12 minutes ago      Exited (0) 9 minutes ago                       charming_jones
```

You can remove container by typing:

```bash
docker rm 30b97ee57158
```

If you want container automatically remove itself after the container in exited status. You can specify `--rm` options when executing the `docker run` command:

```bash
docker run -it --rm busybox sh
```

Also, instead of creating a container for executing the program, we can use `docker exec` to running the program in the current container:

```bash
# Check container id  from existing running containers
docker ps

# Return the result similar as following
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
a843b66bebbe        busybox             "sh"                4 seconds ago       Up 4 seconds                            pensive_carson

# Execute the program using the current container
docker exec -it a843b66bebbe sh
```
