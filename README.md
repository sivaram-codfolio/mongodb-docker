# MongoDB Docker Setup

This repository provides a simple way to run MongoDB using Docker and Docker Compose. The setup includes a single MongoDB instance with configurable environment variables.

## Prerequisites

- Docker installed on your machine
- Docker Compose installed

## Environment Variables

You can configure MongoDB settings using a `.env` file. Create a `.env` file in the project root with the following content:

```
MONGO_CONTAINER_NAME=mongo_db
MONGO_PORT=27017
MONGO_USER=admin
MONGO_PASSWORD=secretpassword
MONGO_DB=mydatabase
```

## Docker Compose Setup

Create a `docker-compose.yml` file with the following content:

```yaml
services:
  mongo:
    image: mongo:6
    container_name: ${MONGO_CONTAINER_NAME}
    restart: always
    environment:
      MONGO_INITDB_ROOT_USERNAME: ${MONGO_USER}
      MONGO_INITDB_ROOT_PASSWORD: ${MONGO_PASSWORD}
      MONGO_INITDB_DATABASE: ${MONGO_DB}
    ports:
      - "${MONGO_PORT}:27017"
    volumes:
      - mongo_db:/data/db
    networks:
      - mongo-network

networks:
  mongo-network:

volumes:
  mongo_db:
```

## Running the Setup

1. **Start MongoDB:**
   ```sh
   docker-compose up -d
   ```

2. **Check running containers:**
   ```sh
   docker ps
   ```

3. **Access MongoDB shell:**
   ```sh
   docker exec -it ${MONGO_CONTAINER_NAME} mongosh -u ${MONGO_USER} -p ${MONGO_PASSWORD}
   ```

## Stopping and Removing the Setup

To stop and remove the MongoDB container, run:

```sh
docker-compose down
```

To remove all data as well:

```sh
docker-compose down -v
```

## Notes

- Data is stored in a Docker volume to persist across restarts.
- You can modify the `.env` file to customize container names, ports, and credentials.
- This setup is intended for development and testing purposes.

---

Feel free to contribute and improve this setup!

