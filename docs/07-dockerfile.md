# Dockerfile

A Dockerfile is a file that contains a set of instructions that describe an environment configuration.

Let try to create rails docker image using `Dockerfile`:

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

```docker
FROM ruby:2.6.3
```

We are using docker image ruby with tag 2.6.3 as the base image for our building our custom image. Visit https://hub.docker.com to see what images are available to choose.