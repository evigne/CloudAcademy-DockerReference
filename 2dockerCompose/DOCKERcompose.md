# Managing Application with Docker Compose

- [Docker Compose Training Github](https://github.com/cloudacademy/docker-compose-training)
  [github](https://github.com/cloudacademy/docker-compose-training/tree/master/multi-env)

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

> ## Compose Commends

- docker-compose #list all possible commends
- docker-compose -f compose-file.yaml up -d #compose the file
- YAML is Data Serialization language (.yaml or .yml)
- we can use JSON or YAML for docker compose

> Data Types

- Integers, strings, NULL (~), Boolean

> Collections

- Mapping (dict), Nested Mapping, Inline Syntax, Sequences(lists), Nested Sequences, sequence in mapping & vice versa.

> Comment

- starts with '#'

> Compose file

- version: '3' # compose relese version file version
- service: services in the application, nested mapping of services under the services key. (eg: web, redis),keys below:
  - image
  - volumes (-v, --mount,--volume)
  - ports (-p) (should be in quots)
  - environment(-e,--env)
  - logging(--log-driver)
  - security_opt
  - command(CMD) it can either written in ['commend', 'commend'] or as a list `- command` \n `- command`
  - depends_on: list the service that the service depends on(first dependent start before the service start)
  - links(express dependencies)
