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
