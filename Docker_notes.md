# Docker in a Month of Lunches

## Chapter 2 - Understanding Docker Notes

1. Docker doesn’t automatically clean up containers or application packages for you.
When you quit Docker Desktop (or stop the Docker service), all your containers stop
and they don’t use any CPU or memory, but if you want to, you can clean up at the
end of every chapter by running this command:

    ```
    docker container rm -f $(docker container ls -aq)
    ```

2. And if you want to reclaim disk space after following the exercises, you can run this
command:

    ```
    docker image rm -f $(docker image ls -f reference='diamol/*' -q)
    ```

3. Connecting to docker container like a remote computer

    ```
    docker container run --interactive --tty name_of_the_container
    ```

    Here *--interactive* flag tells docker that we want to setup a connection to the container and *--ty* flag means we want to connect to the terminal session inside the container.

4. Get details of all the running containers

    ```
    docker ps
    # or  
    docker container ls
    ```
    *docker container ls* only show currently running docker containers.
    If you need all the docker containers irrespective of their status then running the command *docker container ls --all* would give you required results.

5. To list all the process running in the container 

    ```
    docker container top container_id
    ```

6. To display all the log entries the container has collected

    ```
    docker container logs container_id
    ```

7. Starting the containers and running them in the background and communicating between the host computer and docker container

    ```
    docker container run --detach --publish 8088:80 name_of_the_container
    ```

    *--detach* —Starts the container in the background and shows the container ID

    *--publish* —Publishes a port from the container to the computer

    Containers aren’t exposed to the outside world by default. Each has its own IP address, but that’s an IP address that Docker creates for a network that Docker manages—the container is not attached to the physical network of the computer. Publishing a container port means Docker listens for network traffic on the computer port, and then sends it into the container. In the preceding example, traffic sent to the computer on port 8088 will get sent into the container on port 80. 

    Browse to http:/ /localhost:8088 on a browser. That’s an HTTP request to the local computer, but the response comes from the container.

8. To get a live view of how much CPU, memory, network and disk the container is using running the following command

    ```
    docker container stats container_id
    ```

9. When you’re done working with a container, you can remove it with docker container
rm and the container ID, using the --force flag to force removal if the container is
still running.

    ```
    docker container rm --force $(docker container ls --all --quiet)
    ```

10. A short note on the docker architecture

    1. The Docker Engine is the management component of Docker. It looks after the local image cache, downloading images when you need them, and reusing, them if they’re already downloaded. It also works with the operating system to create containers, virtual networks, and all the other Docker resources. The Engine is a background process that is always running (like a Linux daemon or a Windows service).

    1. The Docker Engine makes all the features available through the Docker API, which is just a standard HTTP-based REST API. You can configure the Engine to make the API accessible only from the local computer (which is the default), or make it available to other computers on your network.

    1. The Docker command-line interface (CLI) is a client of the Docker API. When you run Docker commands, the CLI actually sends them to the Docker API, and the Docker Engine does the work.