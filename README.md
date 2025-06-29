# Qdrant Vector Search Engine

This repository contains a Docker Compose setup for running [Qdrant](https://qdrant.tech/), a high-performance vector similarity search engine and vector database.

## What is Qdrant?

Qdrant is a vector similarity search engine designed for production use. It provides a production-ready service with a convenient API to store, search, and manage points (vectors with payload).

### Key Features

- **Vector Search**: Performs high-performance vector similarity search
- **Filtering**: Combines vector search with payload filtering
- **CRUD Operations**: Full-featured API for managing collections, points, and payload
- **Persistence**: Stores all data on disk with the ability to recover from interruptions
- **Distributed**: Scales horizontally to handle large datasets
- **Optimized**: Written in Rust for maximum performance and memory efficiency

## Use Cases

- Semantic search
- Recommendation systems
- Image similarity
- Anomaly detection
- AI applications requiring vector search

## Prerequisites

- Docker and Docker Compose
- At least 1GB of RAM available for the Qdrant container

## Setup Instructions

1. Clone this repository:

   ```bash
   git clone <repository-url>
   cd qdrant-docker-service
   ```

2. Create an environment file from the example:

   ```bash
   cp .env.example .env
   ```

3. (Optional) Configure the API key in the `.env` file:

   ```env
   QDRANT__SERVICE__API_KEY=your-secure-api-key
   ```

4. Make sure you have the `caddy_network` Docker network created:

   ```bash
   docker network create caddy_network
   ```

5. Start the Qdrant service:

   ```bash
   docker-compose up -d
   ```

## Configuration

This setup includes the following configuration:

- **Container Name**: `qdrant`
- **Persistent Storage**: Data is stored in a Docker volume named `qdrant_data`
- **Network**: Connected to `caddy_network` (external network, likely for reverse proxy)
- **Resource Limits**: 1GB memory and 1 CPU
- **Security**: Optional API key authentication

## Accessing Qdrant

- **REST API**: `http://localhost:6333`
- **gRPC API**: `localhost:6334`
- **Web UI**: `http://localhost:6333/dashboard`

## Basic Usage Examples

### Create a Collection

```bash
curl -X PUT 'http://localhost:6333/collections/my_collection' \
    -H 'Content-Type: application/json' \
    -d '{
        "vectors": {
            "size": 768,
            "distance": "Cosine"
        }
    }'
```

### Upload Vectors

```bash
curl -X PUT 'http://localhost:6333/collections/my_collection/points' \
    -H 'Content-Type: application/json' \
    -d '{
        "points": [
            {
                "id": 1,
                "vector": [0.05, 0.61, 0.76, 0.74],
                "payload": {
                    "text": "Sample text",
                    "category": "example"
                }
            }
        ]
    }'
```

### Search for Similar Vectors

```bash
curl -X POST 'http://localhost:6333/collections/my_collection/points/search' \
    -H 'Content-Type: application/json' \
    -d '{
        "vector": [0.05, 0.61, 0.76, 0.74],
        "limit": 3
    }'
```

## Maintenance

### Backup Data

The Qdrant data is stored in the `qdrant_data` Docker volume. To back up this data:

```bash
docker run --rm -v qdrant_data:/data -v $(pwd):/backup alpine tar -czf /backup/qdrant-backup.tar.gz -C /data ./
```

### Restore Data

```bash
docker run --rm -v qdrant_data:/data -v $(pwd):/backup alpine sh -c "rm -rf /data/* && tar -xzf /backup/qdrant-backup.tar.gz -C /data"
```

## Additional Resources

- [Qdrant Documentation](https://qdrant.tech/documentation/)
- [Qdrant GitHub Repository](https://github.com/qdrant/qdrant)
- [Qdrant REST API Reference](https://qdrant.github.io/qdrant/redoc/index.html)
- [Qdrant Python Client](https://github.com/qdrant/qdrant-client)

## License

See the [LICENSE](LICENSE) file for details.
