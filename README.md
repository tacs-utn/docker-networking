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
docker exec backend-for-frontend ip r
docker exec backend ip r
docker exec database ip r
```

### Separate exposing apps from private ones in two different networks:

```
docker-compose -f docker-compose-network.yaml up -d
docker exec gateway curl backend-for-frontend:8080
docker exec gateway curl backend:8080
docker exec gateway curl database:8080
docker exec backend-for-frontend curl backend:8080
docker exec backend-for-frontend curl database:8080
docker exec backend curl database:8080
```
check ips and notice the different network subnets: 

```
docker exec gateway ip r
docker exec backend-for-frontend ip r
docker exec backend ip r
docker exec database ip r
```