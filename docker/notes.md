# Install docker

But first, let's update the package database:

`$sudo yum check-update`

Now run this command. It will add the official Docker repository, download the latest version of Docker, and install it:

`$curl -fsSL https://get.docker.com/ | sh`

After installation has completed, start the Docker daemon:

`$ sudo systemctl start docker`

Verify that it's running:

`$ sudo systemctl status docker`

# Force starting

The following example starts a Redis container and configures it to always restart unless it is explicitly stopped or Docker is restarted.

`$ docker run -dit --restart unless-stopped redis`

# Create interface

`$ docker network create -d bridge --subnet=10.11.0.0/16 ens17 `
or
`$ docker network create --driver=bridge --subnet=172.28.0.0/16 --ip-range=172.28.5.0/24 --gateway=172.28.5.254 br0`

Change name

` $ docker network create --driver=bridge --opt com.docker.network.bridge.name=ens17 --subnet=172.27.0.0/16 --ip-range=172.27.6.0/24 --gateway=172.27.6.254 ens17`

`$ docker network create --driver=bridge --opt com.docker.network.bridge.name=ens18 --subnet=10.11.0.0/16 --ip-range=10.11.1.0/24 --gateway=10.11.1.1 ens18`

# Connect interface

`$ docker container ls`

`$docker run --network=br0 -itd --name=0188e81084fe debian`

`$docker network ls`

`docker network inspect 8b7c3f831f6b`

