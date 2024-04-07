# Commends used

- sudo docker run -it ubuntu /bin/bash #i interactive t sudo tty

- docker start trusting_merkle
- docker attach trusting_merkle # to enter the bash shell of the container
- docker exec -it <mycontainer> bash
- sudo docker container prune #remove all stopped container
- docker build -t greeting .
- docker commit [option] container [repo] #create a image out of container
- docker commit 12jd923n(containterID) #creating image from the container
- docker commit --change='CMD ["python", "-c", "import this"]' 76c9b035829d(ubuntuImage) ubuntu_python # tell image python binary by default -c -> allows arbitary python code to execute
- docker run -d imageId #detached mode # use -dit insteat of -d
- ip addr show #replacement for ifconfig

> ## Detach from container without stopping ctrl+p & ctrl+q

> ## Port Mapping

- docker run -d -P imageName #-P -> publish all, it dynamically bind docker port to host port # use -dit insteat of -d
- docker run -d -p 3000:8080 imageId #docker run -d -p hostPort:containerPort imageID # use -dit insteat of -d

> ## Docker Networking

- docker network ls
- Example

```sh
NETWORK ID     NAME                                                        DRIVER    SCOPE
c7f64d1a2571   bridge                                                      bridge    local
b5894c54f1de   drone_drone-ci-docker-extension-desktop-extension_default   bridge    local
5918cbfd7c55   host                                                        host      local
f948a924827f   none                                                        null      local
2c708568670b   vignesh-sops-test_default                                   bridge    local

```

- all the network on this container `arp-scan --interface=eth0 --localhost`
- bridge: is the default network
- host: add the container to the host newwork
  - if application runs on container port 8080 it gonna bount to port 8080 on host network
  - `docker run -d --network=host ubuntu`
- null: no network completely isolated

> ## Docker Storage

- Three options: Bind Mounts, volumes, In-memory storage (tmpfs)
  > Bind Mounts: mounting file or a directory resid on the host inside of the container it enable to access the host file from container
  - docker build -t "scratch_volume" .
  - docker run -d --mount type=bind, src="/var/demo/logs",dst=/logs scratch_volume #bind mount # use -dit insteat of -d
  - docker run -dit --mount type=bind,src="/Users/vigneshwarane/vigTest",dst="/vigTest" ubuntu # bind host folder with container folder use the same name to work
  - print unique host id in the file `cat /User/vigneshwarane/vigTest | cut -d " " -f 2 | sort | uniq`

```sh
    The command you’ve provided performs a series of text processing operations on the contents of a file located at /User/vigneshwarane/vigTest. Let’s break it down step by step:

    cat /User/vigneshwarane/vigTest:
    cat is a command that concatenates and displays the contents of a file.
    It reads the file located at /User/vigneshwarane/vigTest.
    cut -d " " -f 2:
    cut is used to extract specific columns (fields) from a text file.
    -d " " specifies that the delimiter separating fields is a space.
    -f 2 indicates that we want the second field (column).
    sort:
    sort arranges lines of text in alphabetical or numerical order.
    Since no specific options are provided, it sorts in ascending order.
    uniq:
    uniq filters out adjacent duplicate lines from sorted input.
    It ensures that only unique lines are displayed.
    In summary, this command reads the contents of the file, extracts the second field (assuming fields are separated by spaces), sorts the lines, and then removes any duplicate lines. The result will be a list of unique values from the second field of the file. Keep in mind that the success of this command depends on the structure of the file and the data within it.
```

- > Volumes: like bind mount except Docker manages the storage on the host

  - docker run -dit --mount type=volume,src=my_volume,dst=/vigTest ubuntu #mounting a volume
  - docker volume ls #list all local volums
  - docker volume inspect my_volume #inspect a volume
  - tail -F -s1 /var/lib/docker/volumes/logs/\_data/myapp

```sh
  The command you’ve entered is used for real-time monitoring of log files. Let’s break it down:

tail: This command displays the last few lines of a file.
-f: The -f flag stands for “follow”. It allows you to continuously monitor the file as new lines are added.
-s1: The -s flag specifies the sleep interval (in seconds) between checks for new data. In this case, it’s set to 1 second.
The path you’ve provided (/var/lib/docker/volumes/logs/_data/myapp) points to a Docker volume named logs associated with a container named myapp. If this path is correct, it will display the latest lines from the log file in real-time.
```

- docker ps -aq | sort #sort the container id

- > tmpfs : temporary file system
  - docker run -it --mount type=tmpfs,dst=/logs ubuntu #in memory constuct, everything is temporary

> ## Tagging

- Specific version of image
- docker build -t "tag_demo" .
- docker tag tag_demo:latest tag_demo:v1 # to create a new image from a older image with new tag
- docker tag tag_demo:latest vigneshwarane/tag_demo:latest #tagging with docker user name to push to docker hub
- docker push vigneshwarane/tag_demo:latest # push to registry
