# Dockerfile

A Dockerfile is a file that contains a set of instructions that describe an environment configuration.

Let try to create rails docker image using `Dockerfile`, first create project folder:

```bash
mkdir ~/myapp
cd ~/myapp
```

Create `Dockerfile` with following content in the project root folder:

```docker
FROM ruby:2.6.3

RUN apt-get update -qq && apt-get install -y nodejs postgresql-client yarn

WORKDIR /usr/src/app

COPY Gemfile /usr/src/app
COPY Gemfile.lock /usr/src/app/Gemfile.lock
RUN bundle install

COPY . /usr/src/app

# Add a script to be executed every time the container starts.
COPY entrypoint.sh /usr/bin/
RUN chmod +x /usr/bin/entrypoint.sh
ENTRYPOINT ["entrypoint.sh"]
EXPOSE 3000

# Start the main process.
CMD ["rails", "server", "-b", "0.0.0.0"]
```
Let explain it line by line:

We are using docker image ruby with tag 2.6.3 as the base image to build out our custom image. Visit https://hub.docker.com to see what images are available to choose.

```docker
FROM ruby:2.6.3
```

Then we update the image packages and install nodejs, postgresql-client, and yarn packages for our rails application.


```docker
RUN apt-get update -qq && apt-get install -y nodejs postgresql-client yarn
```

This line set /usr/src/app folder as the workdir inside our image container.

```docker
WORKDIR /usr/src/app
```