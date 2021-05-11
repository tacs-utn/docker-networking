# docker-networking
An example for show how to use docker networking

All containers running in the default network:

`docker-compose up`

Separate exposing apps from private ones in two different networks:

`docker-compose -f docker-compose-network.yaml up`