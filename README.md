# Docker Node.js Development Environment

A Docker Compose-based Node.js development environment with nginx-proxy and Let's Encrypt SSL/TLS support.

## Prerequisites

- Docker
- Docker Compose
- nginx-proxy (running as external network `my_proxy_network`)

## Setup

1. Create `.env` file:

```bash
cp .env.example .env
```

2. Edit `.env` file and configure the required environment variables:

```
CONTAINER_NAME=my_node_app
REPOSITORY=src
DOCKER_PATH=Infra
VIRTUAL_HOST=example.com
VIRTUAL_PORT=3000
LETSENCRYPT_HOST=example.com
LETSENCRYPT_EMAIL=your-email@example.com
LETSENCRYPT_TEST=true
CERT_NAME=default
```

### Environment Variables

- `CONTAINER_NAME`: Docker container name
- `REPOSITORY`: Application source code directory
- `DOCKER_PATH`: Directory containing Dockerfile
- `VIRTUAL_HOST`: Hostname used by nginx-proxy
- `VIRTUAL_PORT`: Port number that the application listens on
- `LETSENCRYPT_HOST`: Domain for SSL certificate
- `LETSENCRYPT_EMAIL`: Email address for Let's Encrypt
- `LETSENCRYPT_TEST`: Set to `true` for testing (use `false` in production)
- `CERT_NAME`: Certificate name

## Usage

### Start containers

```bash
docker-compose up -d
```

### Stop containers

```bash
docker-compose down
```

### View logs

```bash
docker-compose logs -f
```

### Execute commands inside container

```bash
docker-compose exec app sh
```

## Project Structure

```
.
├── Infra/              # Docker related files
│   └── Dockerfile
├── src/                # Application source code
├── docker-compose.yml  # Docker Compose configuration
├── .env.example        # Environment variables template
└── README.md
```

## Networks

This project uses two networks:

- `my_nodejs_network`: Internal network for the application
- `my_proxy_network`: External network for nginx-proxy connection

## Notes

- `my_proxy_network` must be created beforehand
- For production use, set `LETSENCRYPT_TEST` to `false` in `.env`
- SSL certificates are automatically obtained and renewed by Let's Encrypt

## License

MIT License - see [LICENSE](LICENSE) for details

## Author

[takashiraki](https://github.com/takashiraki)