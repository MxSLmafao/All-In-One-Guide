# Ubuntu 22.04 Docker Container Guide

This guide provides step-by-step instructions on how to create and run a **Docker container** with **Ubuntu 22.04**.

## Prerequisites
- Docker installed on your system.
  - **Ubuntu/Debian Install Docker:**
    ```bash
    sudo apt update
    sudo apt install -y docker.io
    sudo systemctl enable --now docker
    ```
  - **Verify Docker Installation:**
    ```bash
    docker --version
    ```

## Step 1: Pull Ubuntu 22.04 Image
Download the official Ubuntu 22.04 image from Docker Hub:

```bash
docker pull ubuntu:22.04
```

## Step 2: Run an Ubuntu 22.04 Container
### Interactive Mode
To run a container interactively:
```bash
docker run -it --name my-ubuntu-container ubuntu:22.04 bash
```

- `-it`: Interactive terminal
- `--name my-ubuntu-container`: Assigns a name to the container (optional)
- `ubuntu:22.04`: Specifies the image
- `bash`: Runs the Bash shell inside the container

### Detached Mode (Background)
To run the container in detached mode:
```bash
docker run -dit --name my-ubuntu-container ubuntu:22.04
```

Attach to it later with:
```bash
docker exec -it my-ubuntu-container bash
```

## Step 3: Managing the Container
### Stop the Container
```bash
docker stop my-ubuntu-container
```

### Start the Container
```bash
docker start -ai my-ubuntu-container
```

### Remove the Container
To delete the container when no longer needed:
```bash
docker rm my-ubuntu-container
```

## Additional Commands
### List Running Containers
```bash
docker ps
```

### List All Containers (Including Stopped)
```bash
docker ps -a
```

### Remove the Ubuntu 22.04 Image
```bash
docker rmi ubuntu:22.04
```

## Conclusion
You now have a fully working Ubuntu 22.04 Docker container. 🚀

For more details, check out [Docker's official documentation](https://docs.docker.com/).
