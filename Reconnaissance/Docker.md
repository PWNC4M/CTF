# Essential Commands

When starting an Attack and Defense (AD) scenario, the first step is to identify the services running within the Vulnerable VM.

## Identifying Docker Services

In the case of Docker, there are two common ways to identify running services:

### 1. Listing Docker Containers

To list all Docker containers (including stopped ones) running on the machine along with their respective ports, use the following command:

```bash
docker ps -a
```

### 2. Inspect docker-compose file
Another method involves inspecting services defined in a docker-compose.yml file. This file specifies the configuration of Docker services and their dependencies.

To inspect the services defined in a docker-compose.yml file and view their configuration details, use the following command:
```bash
docker-compose config
```

