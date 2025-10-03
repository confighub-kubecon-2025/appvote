# AppVote - Example Voting App Helm Chart

A Helm chart for deploying the Example Voting App on Kubernetes.

## Overview

This chart deploys a simple distributed application running across multiple containers:

- **Vote**: A Python webapp which lets you vote between two options
- **Result**: A Node.js webapp which shows the results of the voting in real time
- **Worker**: A .NET worker which consumes votes and stores them in the database
- **Redis**: Redis queue to collect new votes
- **PostgreSQL**: Database backed by a Docker volume

## Installation

```bash
# Install the chart with release name "voting-app"
helm install voting-app .

# Install with custom namespace
helm install voting-app . --namespace voting --create-namespace

# Install with custom values
helm install voting-app . -f custom-values.yaml
```

## Accessing the Application

By default, the services are exposed as NodePort:

- **Vote UI**: http://localhost:31000
- **Result UI**: http://localhost:31001

## Configuration

Key configuration values in `values.yaml`:

### Vote Service
- `vote.replicas`: Number of vote replicas (default: 1)
- `vote.image.repository`: Vote image repository
- `vote.service.type`: Service type (default: NodePort)
- `vote.service.nodePort`: NodePort for vote service (default: 31000)

### Result Service
- `result.replicas`: Number of result replicas (default: 1)
- `result.image.repository`: Result image repository
- `result.service.type`: Service type (default: NodePort)
- `result.service.nodePort`: NodePort for result service (default: 31001)

### Database
- `db.auth.username`: PostgreSQL username (default: postgres)
- `db.auth.password`: PostgreSQL password (default: postgres)
- `db.persistence.enabled`: Enable persistent storage (default: false)

### Redis
- `redis.persistence.enabled`: Enable persistent storage (default: false)

## Uninstalling

```bash
helm uninstall voting-app
```

## Source

Converted from the original Kubernetes manifests at:
https://github.com/dockersamples/example-voting-app
