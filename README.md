# Qdrant Vector Search Engine

This project provides a Docker setup for running Qdrant, a powerful vector search engine designed for high-performance similarity search and retrieval.

## Description

This repository contains Docker configurations to easily deploy Qdrant. Qdrant is an open-source vector search engine that enables you to perform efficient similarity searches on large datasets, making it ideal for applications in machine learning, recommendation systems, and more.

## Services

- **Qdrant**: The main service that runs the Qdrant vector search engine.
  - **Container Name**: qdrant
  - **Image**: qdrant/qdrant
  - **Ports**: Exposed on port (6333)
  - **Volumes**: Data is persisted in `qdrant_data` volume, mapped to `/qdrant/storage`
  - **Environment Variables**: Loaded from `.env`
  - **Restart Policy**: Always restart the container
  - **Resource Limits**: Memory limit of `2G` and CPU limit of `1`

## Installation

1. Clone the repository:

   ```bash
   git clone https://github.com/yourusername/qdrant.git
   ```

2. Navigate to the project directory:

   ```bash
   cd qdrant
   ```

3. Start the services using Docker Compose:

   ```bash
   docker-compose up -d
   ```

## Usage

- Access Qdrant at [http://localhost:6333](http://localhost:6333) to interact with the vector search engine.

## Contributing

1. Fork the repository.
2. Create a new branch:

   ```bash
   git checkout -b feature/YourFeature
   ```

3. Make your changes and commit them:

   ```bash
   git commit -m "Add your message"
   ```

4. Push to the branch:

   ```bash
   git push origin feature/YourFeature
   ```

5. Open a pull request.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
