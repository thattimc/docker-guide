# Dockerfile

A Dockerfile is a file that contains a set of instructions that describe an environment configuration.

Let try to create rails docker image using `Dockerfile`. First, create a project folder:

```bash
mkdir ~/myapp
cd ~/myapp
```

Create `Dockerfile` with the following content in the project root folder:

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

Copy package.json and yarn.lock to project root folder inside the container. Then run `yarn install --check-files` to install npm packages.

```docker
COPY package.json /usr/src/app
COPY yarn.lock /usr/src/app
RUN yarn install --check-files
```

Copy Gemfile, and Gemfile.lock to image first, then run `bundle install` to install ruby gems inside the images. After that copy the remain project files/folders into the image. As docker using layer caching for each `RUN`, `COPY` and `ADD` commands, copy Gemfile and Gemfile.lock before copy entire source code can leverage docker layer caching which in term saving time for install the ruby gem dependencies.

```docker
COPY Gemfile /usr/src/app
COPY Gemfile.lock /usr/src/app/Gemfile.lock
RUN bundle install
COPY . /usr/src/app
```

Now, copy `entrypoint.sh` script to container folder `/usr/bin/` and given the execute permission to that file. Set the `ENTRYPOINT` to run `entrypoint.sh` every time the container startup. Then, expose port 3000 for outside to connect.

```docker
COPY entrypoint.sh /usr/bin/
RUN chmod +x /usr/bin/entrypoint.sh
ENTRYPOINT ["entrypoint.sh"]
EXPOSE 3000
```

Finally, we set the default command to run when no command has specified for running the container.

```docker
CMD ["rails", "server", "-b", "0.0.0.0"]
```

Create an empty `package.json` and `yarn.lock` files

```bash
touch package.json
touch yarn.lock
```

Create a bootstrap `Gemfile` which load Rails. It'll be overwritten in a moment by `rails new`.

```ruby
source 'https://rubygems.org'
gem 'rails', '~> 6.0.0'
```

Create an empty `Gemfile.lock` to build our `Dockerfile`.

```bash
touch Gemfile.lock
```

Next, provide an entrypoint script to fix a Rails-specific issue that prevents the server from restarting when a certain `server.pid` file pre-exists. This script will be executed every time the container gets started. `entrypoint.sh` consists of:

```bash
#!/bin/bash
set -e

# Remove a potentially pre-existing server.pid for Rails.
rm -f /usr/src/app/tmp/pids/server.pid

# Then exec the container's main process (what's set as CMD in the Dockerfile).
exec "$@"
```

Right now we can try to build a docker image and tag it as `myapp`

```bash
docker build -t myapp .
```

You can verify the image by:

```bash
docker images
```

Next: [Docker Compose](08-docker-compose.md)