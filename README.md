# docker-networking
An example for show how to use docker networking

### All containers running in the default network:

```
docker-compose up -d
docker exec gateway curl backend-for-frontend:8080
docker exec gateway curl backend:8080
docker exec gateway curl database:8080
```

check ips and notice the default network subnet: 

```
docker exec gateway ip r
docker exec docker-networking_backend-for-frontend_1 ip r
docker exec docker-networking_backend_1 ip r
docker exec database ip r
```

### Separate exposing apps from private ones in two or more different networks:

```
docker-compose -f docker-compose-network.yaml up -d
docker exec gateway curl backend-for-frontend:8080
docker exec gateway curl backend:8080
docker exec gateway curl database:8080
docker exec docker-networking_backend-for-frontend_1 curl backend:8080
docker exec docker-networking_backend-for-frontend_1 curl database:8080
docker exec docker-networking_backend_1 curl database:8080
```
check ips and notice the different network subnets: 

```
docker exec gateway ip r
docker exec docker-networking_backend-for-frontend_1 ip r
docker exec docker-networking_backend_1 ip r
docker exec database ip r
```


## Docker-compose Scale and Balanced Service Resolver

```
docker-compose -f docker-compose-network.yaml up -d
docker-compose scale backend-for-frontend=5 backend=3
```

check different ips on service discovery balancing:

```
(repeat x5) docker exec gateway ping backend-for-frontend -c 1
(repeat x3) docker exec docker-networking_backend-for-frontend_1 ping backend -c 1
```

## References
- https://docs.docker.com/compose/networking/
- https://docs.docker.com/compose/reference/scale/
- https://docs.docker.com/compose/compose-file/compose-file-v3/#container_name

