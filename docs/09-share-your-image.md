# Share Your Image

If you follow along with labs, you should have a custom docker image created in your local machine. To share it to the world or your team members, you need to push it to the docker hub or any other Docker registry such as Amazon Elastic Container Registry (ECR) or Google Container Registry.

However, for this lab, we will use the docker hub for storing our custom image as it's free and allow storing one private image repository.

Log in to the Docker public registry on your local machine.

```bash
docker login
```

Tag the image using the format like this

```bash
docker tag image username/repository:tag
```

For instance:

```bash
docker tag myapp timshingyu/myapp:v1.0.0
```

To review the newly tagged image:

```bash
docker images
```

Upload your tagged image to the repository:

```bash
docker push timshingyu/myapp:v1.0.0
```

You can review the image by login to your docker hub account.

Now, you can pull and run the image from the remote repository:

```bash
docker run -p 3000:3000 timshingyu/myapp:v1.0.0
```