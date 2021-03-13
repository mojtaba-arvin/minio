# Simple S3-compatible object storage service using Minio
![minio up](https://user-images.githubusercontent.com/6056661/111041989-4da76c00-8450-11eb-9a84-9ae00740d024.png)
### Setup environment

`Minio` environment ,must be at `.docker-compose/` directory as `.env` file. you can copy the sample:
```
cp .docker-compose/.env.local .docker-compose/.env
```

### Minio UI Access

#### production
To use Minio in production, there is a sample compose file ( `docker-compose.join.nginx.yml` ) , to join `Nginx` reverse proxy network.
you can use docker-compose `-f` option, to join nginx network

```
docker-compose -f docker-compose.yml -f docker-compose.join.nginx.yml up -d
```
then, you can use Nginx `upstream` to load balancing all instances through port `9000`
#### development
In local environment, there is a sample compose file ( `docker-compose.local.yml` ), to map ports.

```
docker-compose -f docker-compose.yml -f docker-compose.join.local.yml up -d
```

then, the Minio UI can be accessed using a Web browser at `http://localhost:9000/`.

### Clients

Clients on the same machine, can join this service by define an external network,
for example when the client network name is `sample-network` it should define as:

```
networks:
    sample-network:
        external:
            name: minio_object-storage-network
```

The `external` network name, has two part, which are separated by an underline, `minio` is name of the repository, and `object-storage-network` is the network name of this repository
