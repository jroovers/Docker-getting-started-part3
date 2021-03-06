# Getting started with docker part 3

https://docs.docker.com/get-started/part3/

>The **docker-compose.yml** file tells Docker to do the following:
>
>* Pull the image we uploaded in step 2 from the registry.
>* Run 5 instances of that image as a service called web, limiting each one to use, at most, 10% of a single core of CPU time (this could also be e.g. “1.5” to mean 1 and half core for each), and 50MB of RAM.
>* Immediately restart containers if one fails.
>* Map port 4000 on the host to web’s port 80.
>* Instruct web’s containers to share port 80 via a load-balanced network called webnet. (Internally, the containers themselves publish to web’s port 80 at an ephemeral port.)
>* Define the webnet network with the default settings (which is a load-balanced overlay network).

## Run this load-balanced app

```bash
# start a swarm
docker swarm init
# deploy a stack. 
# -c points to the docker-compose file. 
# getstartedlab is the name of this app.
docker stack deploy -c docker-compose.yml getstartedlab
```

You can now view the app in your browser at your docker-machine's ip.

### Other commands
```bash
# Show all containers in service (jargon: TASK)
docker stack ps getstartedlab
# Update the stack with the same command as starting it.
# for example, after increasing the replica count.
docker stack deploy -c docker-compose.yml getstartedlab
```

### Cleaning up

```bash
# Take down the app
docker stack rm getstartedlab
# Take down the swarm
docker swarm leave --force
```