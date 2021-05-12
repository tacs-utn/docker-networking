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

### Separate exposing apps from private ones in two different networks:

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