# Rust OpenFHE Development Environment

This project provides a Docker-based development environment for Rust and OpenFHE. This environment is suitable for x86_64 architecture and can run on Apple Silicon (M1) Macs.

## Prerequisites

- Install [Docker Desktop](https://www.docker.com/products/docker-desktop)
- If using an M1 Mac, ensure Rosetta 2 is enabled to support x86_64 emulation

## Setting up the Development Environment

1. Clone this repository:
   ```
   git clone <your-repository-url>
   cd <your-repository-name>
   ```

2. Build the Docker image:
   ```
   docker build -t rust-openfhe-dev -f .devcontainer/Dockerfile .
   ```

3. Run the Docker container:
   ```
   docker run -it --rm --platform linux/amd64 -v $(pwd):/workspace -w /workspace rust-openfhe-dev bash
   ```

   This command will:
   - Run the container using the x86_64 platform
   - Mount the current directory to the `/workspace` directory in the container
   - Open a bash shell inside the container
   - Automatically remove the container when you exit

## Development Workflow

1. Start a new container instance to compile and run the code:
   ```
   docker run -it --rm --platform linux/amd64 -v $(pwd):/workspace -w /workspace rust-openfhe-dev bash
   ```

2. Compile and run the code inside the container:
   ```
   cargo build
   cargo run
   ```

3. When finished, type `exit` or press Ctrl+D to exit the container. The container will be automatically removed, but your local file changes will be preserved.
