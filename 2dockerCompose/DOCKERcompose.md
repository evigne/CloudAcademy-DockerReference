# Managing Application with Docker Compose

- [Docker Compose Training Github](https://github.com/cloudacademy/docker-compose-training)
  [github](https://github.com/cloudacademy/docker-compose-training/tree/master/multi-env)
  [DockerComposeDOC](https://docs.docker.com/compose/)

> ## Before Docker compose

- docker network create --driver bridge app_network
- docker volume create serviceB_volume
- docker build -f Dockerfile.serviceA .
- docker build -f Dockerfile.serviceB .
- docker run -d -name serviceA --network app_network -p 8080:3000 serviceA
- docker run -d -name serviceB --network app_network --mount source=serviceB_volume,target=/data serviceB
- docker stop serviceA serviceB
- docker rm serviceA serviceB
- docker rmi serivceA serviceB
- docker volume rm serviceB_volume
- docker network rm app_network

> ## Compose Commands

- docker-compose #list all possible commands
- docker-compose -f compose-file.yaml up -d #compose the file
- YAML is Data Serialization language (.yaml or .yml)
- we can use JSON or YAML for docker compose

> Data Types

- Integers, strings, NULL (~), Boolean

> Collections

- Mapping (dict), Nested Mapping, Inline Syntax, Sequences(lists), Nested Sequences, sequence in mapping & vice versa.

> Comment

- starts with '#'

> Compose file YAML file

- version: '3' # compose relese version file version
- service: services in the application, nested mapping of services under the services key. (eg: web, redis),keys below:
  - image
  - volumes (-v, --mount,--volume)
  - ports (-p) (should be in quots)
  - environment(-e,--env)
  - logging(--log-driver)
  - security_opt
  - command(CMD) it can either written in ['command', 'command'] or as a list `- command` \n `- command`
  - depends_on: list the service that the service depends on(first dependent start before the service start)
  - links(express dependencies)
  - Network
  - Extension Fields - Reuse configuration fragments =>check this only available from verison 3.4 **\***

> Compose File Commands

- docker-compose [option] [command] [args]
- Connects to Docker Deamon on the host by default
- - can connect to remote hosts with -H
- - secure remote connections wiht --tls options
- looks for docker-compose.(yml | yaml), or specify file name with -f
- Projects to represent isolated app
- - default uses directory as project name
- - use -p to specify custom names

> docker-compose command

- docker commands
- - build, config, create, events, exec, images , kill,logs, pause, port, ps, pull, push, restart, rm ,run, start
- - stop, top, unpause, version
- docker compose commands
- - up => create newtork and named volumes, build, creates, starts and attaches to service container
- - down => removes service container, but leaves volumes and images by default
