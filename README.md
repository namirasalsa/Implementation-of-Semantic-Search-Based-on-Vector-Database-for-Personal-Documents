# Semantic Search Implementation with Milvus for Personal Documents

## Overview
Milvus is a high-performance, scalable vector database designed for various use cases, from small demos to large-scale enterprise systems. It offers three deployment options:

- **Milvus Lite**: Lightweight, ideal for prototyping.
- **Milvus Standalone**: Single-machine deployment for production workloads.
- **Milvus Distributed**: Scalable Kubernetes-based deployment for large-scale systems.

For this project, "**Implementation of Semantic Search with Vector Database for Personal Documents**," Milvus Standalone is used for its simplicity and production-ready capabilities.

---

## Prerequisites

1. **Install Docker Desktop** 🐋
   - [Download Docker Desktop](https://www.docker.com/products/docker-desktop).
   - Run Docker Desktop as an administrator.
2. **Install WSL 2** 🖥️
   - Follow the [official guide](https://learn.microsoft.com/en-us/windows/wsl/install) to enable Windows Subsystem for Linux 2.
3. **Install Python** 🐍
   - Download Python 3.8+ from the [official website](https://www.python.org/downloads/).

---

## Steps to Deploy Milvus Standalone (Run Milvus in Docker on Windows)

### 1. Download and Run the Installation Script

1. Open **PowerShell** or **Command Prompt** in administrator mode.
2. Download the installation script:

   ```powershell
   Invoke-WebRequest https://raw.githubusercontent.com/milvus-io/milvus/refs/heads/master/scripts/standalone_embed.bat -OutFile standalone.bat
   ```

3. Start Milvus using the downloaded script:

   ```powershell
   standalone.bat start
   ```

   - Wait for the message: `Start successfully.`
   - Milvus will run as a Docker container named `milvus-standalone` at port **19530**.

### 2. Configuration and Data Mapping

- **Default Configuration**: The configuration file `user.yaml` is located in the current folder.
- **Embedded etcd**: Installed within the same container and serves at port **2379**. Configuration file: `embedEtcd.yaml`.
- **Data Volume**: Milvus data is mapped to `volumes/milvus` in the current folder.

### 3. Manage Milvus

Use the following commands to manage the Milvus container and its data:

- **Stop Milvus**:
  ```powershell
  standalone.bat stop
  ```
  Output: `Stop successfully.`

- **Delete Milvus Container**:
  ```powershell
  standalone.bat delete
  ```
  Output:
  - `Delete Milvus container successfully.`
  - `Delete successfully.` (Data has been removed.)

---

## Verify Installation

1. **Check Docker Container**:
   ```powershell
   docker ps
   ```
   Ensure `milvus-standalone` is running.

2. **Test Milvus Connection**:
   Install the Python client library and test connectivity:
   ```bash
   pip install pymilvus
   ```
   ```python
   from pymilvus import connections

   connections.connect("default", host="127.0.0.1", port="19530")
   print("Connected to Milvus successfully!")
   ```

---

## Execute the Program

### 1. Download and Extract Dataset

1. Download the dataset `personaldocumentsdataset.zip` from this repository.
2. Extract the ZIP file to a directory on your local machine (e.g., `C:\datasets\personaldocuments`).

### 2. Install Required Libraries

Ensure Python 3.10 is installed. Then, install the necessary libraries using the command below:

```bash
pip install fitz pymilvus numpy python-docx tempfile reportlab sentence-transformers
```

### 3. Adjust Dataset Path in Code

If the extracted dataset path is different from the one specified in `code.ipynb`, update the path accordingly in the code. For example:

```python
DATASET_PATH = "C:\\datasets\\personaldocuments"
```

### 4. Execute the Program

Open `code.ipynb` in Jupyter Notebook or any compatible environment and run the cells sequentially to execute the program.

---

## Additional Resources

- [Milvus Official Documentation](https://milvus.io/docs/)
- [Docker Documentation](https://docs.docker.com/)

---

If you enjoyed this project, please consider starring ⭐ the repository and following me on GitHub for more exciting projects! 🚀

