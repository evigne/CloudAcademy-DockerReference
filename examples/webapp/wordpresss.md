> # Commands

- - > run in detached mode
- docker-compose -f wordpress.yml up -d

- - > only bring up the service we want
- docker-compose -f wordpress.yml up -d --no-deps wordpress

- - > force recreate even if there is no change
- docker-compose -f wordpress.yml up -d --force-recreate

- - > bring down the services in the compose file [leves the volumes untouched]
- docker-compose -f wordpress.yml down

- - > delete volume and images
- docker-compose -f wordpress.yml down -rmi all --volumes --remove-orphanes
