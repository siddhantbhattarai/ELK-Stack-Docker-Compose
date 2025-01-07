# ELK Stack Docker Compose

This repository provides a quick and easy setup for running an **ELK (Elasticsearch, Logstash, Kibana)** stack using **Docker Compose**. The stack is configured to ingest, process, and visualize logs using the provided configuration files.

---

## Table of Contents
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Directory Structure](#directory-structure)
- [Configuration](#configuration)
- [Usage](#usage)
- [Stopping the Stack](#stopping-the-stack)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)
- [License](#license)

---

## Prerequisites

Before running the ELK stack, ensure that you have the following installed on your system:

- [Docker](https://www.docker.com/products/docker-desktop/)
- [Docker Compose](https://docs.docker.com/compose/install/)

You can check the installed versions by running:
```bash
$ docker --version
$ docker-compose --version
```

---

## Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/siddhantbhattarai/ELK-Stack-Docker-Compose.git
   ```
2. Navigate to the cloned directory:
   ```bash
   cd ELK-Stack-Docker-Compose
   ```

---

## Directory Structure

The repository is structured as follows:

```
repo/
├── docker-compose.yml  # Defines the ELK services
└── logstash/
    └── pipeline/
        └── logstash.conf  # Logstash pipeline configuration
```

### Explanation:
- `docker-compose.yml`: Contains service definitions for **Elasticsearch**, **Logstash**, and **Kibana**.
- `logstash.conf`: Defines how Logstash processes incoming log data (e.g., inputs, filters, outputs).

---

## Configuration

### Logstash Pipeline Configuration (`logstash.conf`)
You can customize the `logstash.conf` file to suit your logging needs. Below is an example configuration:

```plaintext
input {
  beats {
    port => 5044
  }
}

filter {
  # Example filter (optional)
}

output {
  elasticsearch {
    hosts => ["elasticsearch:9200"]
    index => "logs-%{+YYYY.MM.dd}"
  }
  stdout { codec => rubydebug }
}
```

Modify the `input`, `filter`, and `output` sections as required.

---

## Usage

1. Start the ELK Stack:
   ```bash
   docker-compose up -d
   ```
   This will start the Elasticsearch, Logstash, and Kibana containers in detached mode.

2. Verify that the services are running:
   ```bash
   docker ps
   ```

3. Access Kibana in your web browser at:
   ```
   http://localhost:5601
   ```

4. In Kibana, you can create an index pattern to view your log data.

---

## Stopping the Stack

To stop and remove the containers:
```bash
docker-compose down
```

If you want to remove volumes and networks:
```bash
docker-compose down -v
```

---

## Troubleshooting

### Common Issues:
- **Elasticsearch fails to start:** Ensure you have at least 4GB of memory allocated to Docker.
- **Permission Denied:** Run with elevated permissions or configure Docker for non-root usage.

To view container logs:
```bash
# View logs of a specific service
docker-compose logs [service-name]
```

---

## Contributing

Contributions are welcome! Feel free to open an issue or submit a pull request if you have improvements.

---

## License

This project is licensed under the MIT License. See the `LICENSE` file for details.
