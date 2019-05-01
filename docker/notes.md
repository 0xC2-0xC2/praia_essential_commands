# install docker

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
