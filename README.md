# MCP Deployment Configurator

Welcome to the **MCP Deployment Configurator**! This project demonstrates how to expose Infrastructure-as-Code (IaC) templates via the open **Model Context Protocol (MCP)**, enabling Large Language Models (LLMs) to list, read, parameterize, and apply infrastructure configurations interactively.

## Features

- **Discover** available IaC modules (Terraform & Kubernetes) organized under `modules/`.
- **Read** template files (`.tf`, `.yaml`) on demand.
- **Generate** parameterized configurations by writing variable definitions to a temporary directory.
- **Apply** or **plan** infrastructure changes using Terraform CLI.
- **Dockerized**: ready to run in a container.
- **CI/CD**: sample GitHub Actions pipeline for testing and Docker image publishing.

## Repository Structure
```text
mcp-deployment-configurator/
├── modules/
│   ├── terraform/
│   │   ├── vpc/
│   │   │   ├── main.tf
│   │   │   ├── variables.tf
│   │   │   └── outputs.tf
│   │   └── kubernetes-cluster/
│   │       └── main.tf
│   └── kubernetes/
│       └── nginx-deployment.yaml
├── server/
│   ├── __init__.py
│   ├── main.py
│   └── tools.py
├── Dockerfile
├── requirements.txt
├── .gitignore
└── README.md
```

## Prerequisites

- **Python 3.11+**
- **Terraform CLI** installed (for local testing)
- **Docker** (optional, to run in a container)

## Quickstart

### 1. Clone the repository
```bash
git clone https://github.com/your-username/mcp-deployment-configurator.git
cd mcp-deployment-configurator
```

### 2. Python setup
```bash
python3 -m venv venv
source venv/bin/activate
echo "mcp[cli]" > requirements.txt
pip install -r requirements.txt
```

### 3. Run the MCP server
```bash
python server/main.py
```

### 4. Interact via SSE/JSON-RPC
Use `curl` or your LLM client:
```bash
curl http://localhost:8080/mcp -N -H "Accept: text/event-stream" --data '{"jsonrpc":"2.0","method":"tools/list_templates","id":1}'
```

## Docker

Build and run:
```bash
docker build -t mcp-deployment-configurator .
docker run -p 8080:8080 mcp-deployment-configurator
```

## CI/CD

A sample GitHub Actions workflow (`.github/workflows/ci.yml`) runs tests, lints code, and builds/publishes the Docker image on each push.

## Contributing

Contributions welcome! Feel free to open issues or pull requests to add new modules, improve functionality, or fix bugs.

## License

MIT License. See [LICENSE](LICENSE) for details.
