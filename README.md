## Getting Started

### Prerequisites

Make sure you have the following prerequisites installed on your machine:

- Docker (should also be able to run docker compose ...)

#### GPU Support (Optional)

If you have a GPU and want to leverage its power within a Docker container, follow these steps to install the NVIDIA Container Toolkit:

```bash
curl -fsSL https://nvidia.github.io/libnvidia-container/gpgkey | sudo gpg --dearmor -o /usr/share/keyrings/nvidia-container-toolkit-keyring.gpg \
  && curl -s -L https://nvidia.github.io/libnvidia-container/stable/deb/nvidia-container-toolkit.list | \
    sed 's#deb https://#deb [signed-by=/usr/share/keyrings/nvidia-container-toolkit-keyring.gpg] https://#g' | \
    sudo tee /etc/apt/sources.list.d/nvidia-container-toolkit.list
sudo apt-get update
sudo apt-get install -y nvidia-container-toolkit

# Configure NVIDIA Container Toolkit
sudo nvidia-ctk runtime configure --runtime=docker
sudo systemctl restart docker

# Test GPU integration
docker run --gpus all nvidia/cuda:11.5.2-base-ubuntu20.04 nvidia-smi
```

### Configuration

1. Clone the Docker Compose repository:

   ```bash
   gh repo clone amusement-lab/ollama-docker
   ```

2. Change to the project directory:

   ```bash
   cd ollama-docker
   ```

### Usage

Start Ollama and its dependencies using Docker Compose:

if gpu is configured

```bash
docker compose -f docker-compose-ollama-gpu.yaml up -d
```

else

```bash
docker compose up -d
```

### Note

Source https://github.com/mythrantic/ollama-docker
