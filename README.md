# NESA-NODE
RUN A NESA NODE
# Prerequisites

{% hint style="warning" %}
**Note:** This software is in **beta** and primarily targets **Ubuntu/Debian** machines with **CUDA**-enabled GPUs. Support for other hardware/software configurations is **experimental** and will improve over time.
{% endhint %}

### Introduction

Before running a Nesa node, ensure your system meets the following prerequisites. This will help you set up and run the node smoothly.

***

### System Requirements

**Hardware Recommendations**

* **CPU**: Multi-core processor
* **Memory**: 4 GB RAM minimum
* **Storage**: 50 GB free disk space (or more depending on the size of the model(s) you'd like to power)
* **Network**: Stable internet connection

{% hint style="info" %}
**Note:** Miner nodes operate optimally with high-performance graphics hardware.
{% endhint %}

**Supported Operating Systems**

* Linux (Ubuntu, Debian, CentOS, etc.)
* macOS
* Windows (with WSL recommended)

### Software Requirements

**Required Software**

* **GPU Drivers:** Required for hardware acceleration. Please consult your GPU manufacturer's website for reference.
* **Nvidia Toolkit:** Applicable to machines with an NVIDIA graphics card. [Install Toolkit](https://github.com/nesaorg/bootstrap/blob/master/helpers/install_nvidia_container_toolkit.sh)
* **Docker**: Required to run the node. [Install Docker](https://docs.docker.com/get-docker/)

  ```bash
  # Example command to install Docker on Debian/Ubuntu
    # Add Docker's official GPG key:
    sudo apt-get update
    sudo apt-get install ca-certificates curl
    sudo install -m 0755 -d /etc/apt/keyrings
    sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
    sudo chmod a+r /etc/apt/keyrings/docker.asc
    
    # Add the repository to APT sources:
    echo \
      "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
      $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
      sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
    sudo apt-get update
    sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
  ```

  ```bash
  # Example command to install Docker on macOS using Homebrew
  brew install --cask docker
  ```

  ```powershell
  # Example command to install Docker on Windows using PowerShell
  choco install docker-desktop
  ```
* **curl**: Required to fetch the bootstrap script. [Install curl](https://curl.se/docs/install.html)

  ```bash
  # Example command to install curl on Ubuntu
  sudo apt-get update
  sudo apt-get install -y curl
  ```

  ```bash
  # Example command to install curl on macOS using Homebrew
  brew install curl
  ```

  ```powershell
  # Example command to install curl on Windows using PowerShell
  choco install curl
  ```

**Installing Necessary Dependencies**

* **gum**: The script installs gum if not present.
* **jq**: The script installs jq if not present.

  ```bash
  # Command to check if jq is installed
  jq --version

  # If jq is not installed, the script will attempt to install it
  ```

### Account and Token Requirements

**Hugging Face API Token**

You will need a Hugging Face API token. [Get your token here](https://huggingface.co/docs/hub/security-tokens).

{% hint style="info" %}
**Hint**: Make sure to save your Hugging Face API token securely. You will need it during setup.
{% endhint %}

**Moniker for Your Node**

Decide on a unique name (moniker) for your node.

{% hint style="info" %}
**Hint**: Choose a moniker that reflects the identity of your node within the network.
{% endhint %}

**Node Type Selection**

Decide whether your node will be a Validator or a Miner. Validators participate in consensus, while Miners handle inference tasks.

**Validator**

* **Role**: Validators are responsible for verifying transactions, creating new blocks, and maintaining the security and integrity of the blockchain.
* **Tasks**: Participate in the consensus process, validate transactions and blocks, and earn rewards for their services.
* **Requirements**: Require a stable internet connection and typically less less computational power than miner nodes. In a PoS network, they also stake tokens as collateral.

**Miner**

* **Role**: Miners execute the heavy-lifting components of AI inference.
* **Tasks**: Collect and verify transactions, bundle them into blocks, and earn rewards for successfully adding blocks to the blockchain.
* **Types**:
  * **Distributed Miner**: Joins existing swarms for collaborative mining.
  * **Non-Distributed Miner**: Operates independently without collaboration.
* **Requirements**: Vary depending on whether they are distributed or non-distributed. Both types require good computational power and internet stability.

### Administrative Rights

Ensure you have administrative rights on your system.

**Linux/macOS**

You should have the ability to use `sudo` for installing packages and running Docker.

{% hint style="info" %}
For linux-based systems, ensure your user is part of the `docker` group by running the following commands:
{% endhint %}

```bash
# Create a docker group (if non-existent), adds the current user, 
# and applies group membership immediately in the current session
sudo groupadd docker
sudo usermod -aG docker $USER
newgrp docker
```

{% hint style="info" %}
**Hint**: To check if you have sudo privileges, run the following command:
{% endhint %}

```bash
sudo -v
```

**Windows**

You should have an administrator account or use WSL with administrative privileges.

{% hint style="info" %}
**Hint**: On Windows, you can check if you are an administrator by going to Control Panel > User Accounts > Manage User Accounts.
{% endhint %}

***

### Additional Help/Support

If you need any additional help or support, please visit the [Nesa Discord](https://discord.gg/nesa) for community support and discussion. You can also explore additional documentation to deepen your understanding of Nesa and its features.



***

# Installation

### Introduction

This guide will walk you through the installation process for running a Nesa node.

***

### Download and Execute the Bootstrap Script

To download and run the bootstrap script, use the following command:

<pre class="language-bash"><code class="lang-bash"># For all operating systems
<strong>bash &#x3C;(curl -s https://raw.githubusercontent.com/nesaorg/bootstrap/master/bootstrap.sh)
</strong></code></pre>

{% hint style="info" %}
**Hint**: Ensure Docker is running before executing the script.
{% endhint %}

{% hint style="info" %}
**View Your Node's Performance**

Visit <https://node.nesa.ai> and enter your Node ID.

You can find your Node ID by re-running the bootstrap script (above) and reading the Node ID from the script's header.
{% endhint %}

***

### Node Configuration

During the script execution, you will be prompted to configure your node:

1. **Moniker**: Choose a unique name for your node.

   ```bash
   # Example prompt
   Choose a moniker for your node: <Your Node Name>
   ```
2. **Node Type**: Select whether your node will be a Validator or a Miner.

   ```bash
   # Example prompt
   What type(s) of node is <Your Node Name>?
   [ ] Validator
   [ ] Miner
   ```

   * **Validator**: Enter the private key for the validator.

     ```bash
     # Example prompt
     Validator's Private Key: <Your Private Key>
     ```
   * **Miner**:
     * **Miner Type**: Choose between Distributed Miner or Non-Distributed Miner.

       ```bash
       # Example prompt
       What type of miner will <Your Node Name> be?
       [ ] Distributed Miner
       [ ] Non-Distributed Miner
       ```
     * **Model Selection**:
       * For Distributed Miner: Select an existing swarm or start a new one.

         ```bash
         # Example prompt for Distributed Miner
         Would you like to join an existing swarm or start a new one?
         [ ] Join existing swarm
         [ ] Start a new swarm
         ```

         If starting a new swarm:

         ```bash
         # Example prompt
         Which model would you like to run? (meta-llama/Llama-2-13b-Chat-Hf)
         ```
       * For Non-Distributed Miner: Enter the model name to run.

         ```bash
         # Example prompt for Non-Distributed Miner
         Which model would you like to run? (meta-llama/Llama-2-13b-Chat-Hf)
         ```

### **Understanding Swarms**

A swarm in the context of Nesa is an orchestrator with one or more miners working collaboratively to handle inference tasks. Distributed miners can join an existing swarm to contribute to an ongoing effort or start a new swarm to initiate a new collaborative mining process.

**Swarm Configuration Process**:

1. **Select an Existing Swarm**:
   * You will be presented with a list of available swarms.
   * Select the swarm you want to join.
   * The script will configure your node to connect to the selected swarm.
2. **Start a New Swarm**:
   * Enter the model name you want to run.
   * The script will set up a new swarm for this model.
   * Your node will act as the initial member of this new swarm, and others can join later.

***

### Final Setup

After completing the configuration:

1. The script will set up the working directory and clone the necessary repositories.
2. Docker containers will be started using `docker-compose`.

To check the status of your node:

```bash
# Check Docker containers status
docker ps
```

{% hint style="info" %}
**Note**: Ensure all required Docker containers are running.
{% endhint %}

***

#### Additional Help/Support

If you need any additional help or support, please visit the [Nesa Discord](https://discord.gg/nesa) for community support and discussion. You can also explore additional documentation to deepen your understanding of Nesa and its features.



***


# Troubleshooting

### Introduction

This section provides solutions to common issues encountered during the installation and operation of a Nesa node.

***

### Script Fails to Download or Execute

**Possible Reasons and Solutions**:

* **Network Issues**: Ensure your internet connection is stable.
* **Incorrect Command**: Verify the command syntax.

**Steps to Verify and Fix**:

**Linux/macOS**

```bash
# Check network connectivity
ping google.com

# Verify curl installation
curl --version

# Correct command to download and execute the script
curl -L https://raw.githubusercontent.com/nesaorg/bootstrap/master/bootstrap.sh | bash
```

**Windows (WSL)**

```bash
# Check network connectivity
ping google.com

# Verify curl installation
curl --version

# Correct command to download and execute the script
curl -L https://raw.githubusercontent.com/nesaorg/bootstrap/master/bootstrap.sh | bash
```

***

### Permission Denied Errors

**Explanation of Permission Issues**:

* Insufficient permissions to execute the script or install software.

**Resolution Steps**:

**Linux/macOS**

```bash
# Ensure the script is executable
chmod +x bootstrap.sh

# Run the script with sudo
sudo ./bootstrap.sh
```

**Windows (WSL)**

```bash
# Ensure the script is executable
chmod +x bootstrap.sh

# Run the script with elevated privileges
sudo ./bootstrap.sh
```

***

### Docker-Related Issues

**Common Issues and Solutions**:

* **Docker Not Running**: Ensure Docker service is active.
* **Installation Issues**: Reinstall Docker if necessary.

**Verify Docker Installation and Status**:

**Linux/macOS**

```bash
# Check Docker version
docker --version

# Start Docker service
sudo systemctl start docker

# Verify Docker service status
sudo systemctl status docker
```

**Windows (WSL)**

```powershell
# Check Docker version
docker --version

# Start Docker service from Docker Desktop
Start-Process 'C:\Program Files\Docker\Docker\Docker Desktop.exe'
```

***

### Node Configuration Problems

**Troubleshooting Configuration Issues**:

* Incorrect moniker or node type selection.

**Reconfiguration Steps**:

```bash
# Rerun the script to reconfigure the node
./bootstrap.sh
```

***

### Connectivity Issues

**Diagnosing Network Problems**:

* **Firewall Restrictions**: Ensure necessary ports are open.
* **Network Configuration**: Verify network settings.

**Steps to Fix Connectivity Issues**:

**Linux/macOS**

```bash
# Check open ports
sudo ufw status

# Allow necessary ports (example for port 26656)
sudo ufw allow 26656
```

**Windows (WSL)**

```powershell
# Check open ports in Windows Firewall
Get-NetFirewallRule -All

# Allow necessary ports (example for port 26656)
New-NetFirewallRule -DisplayName "Allow Nesa Node" -Direction Inbound -Protocol TCP -LocalPort 26656 -Action Allow
```

***

#### Additional Help/Support

If you need any additional help or support, please visit the [Nesa Discord](https://discord.gg/nesa) for community support and discussion. You can also explore additional documentation to deepen your understanding of Nesa and its features.


***


# FAQ

### Introduction

This section addresses common questions about setting up and running a Nesa node.

***

### **What is a Nesa node?**

A Nesa node is a server that participates in the Nesa blockchain network, either by validating transactions (Validator) or by handling inference tasks for AI models (Miner).

### **What are the hardware requirements for running a Nesa node?**

* **CPU**: Multi-core processor
* **Memory**: 4 GB RAM minimum
* **Storage**: 50 GB free disk space (or more depending on the size of the model(s) you plan to power)

### **How do I view my node's performance?**

Visit <https://node.nesa.ai> and enter your Node ID.

You can find your Node ID by re-running the [bootstrap script](https://docs.nesa.ai/nesa/run-a-nesa-node/installation) and reading it from the script's header.

### **How do I install Docker?**

* **Linux**:

  ```bash
  # Add Docker's official GPG key:
  sudo apt-get update
  sudo apt-get install ca-certificates curl
  sudo install -m 0755 -d /etc/apt/keyrings
  sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
  sudo chmod a+r /etc/apt/keyrings/docker.asc
    
  # Add the repository to APT sources:
  echo \
    "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
    $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
    sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
  sudo apt-get update
  sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
  # Example command to install Docker on macOS using Homebrew
  brew install --cask docker
  # Example command to install Docker on Windows using PowerShell
  choco install docker-desktop
  ```
* **macOS**:

  ```bash
  brew install --cask docker
  ```
* **Windows (WSL)**:

  ```powershell
  choco install docker-desktop
  ```

### **How do I configure my node as a Validator or Miner?**

During the bootstrap script execution, you will be prompted to select a node type:

* **Validator**: Enter the private key for the validator.
* **Miner**: Choose between Distributed Miner or Non-Distributed Miner, and select or enter a model.

### **What should I do if the bootstrap script fails to run?**

* **Verify network connectivity**
* **Check curl installation**
* **Run the script with appropriate permissions**

```bash
# For all operating systems
curl -L https://raw.githubusercontent.com/nesaorg/bootstrap/master/bootstrap.sh | bash
```

### **How do I check if my node is running correctly?**

Verify Docker containers status:

```bash
docker ps
```

Ensure all required Docker containers are running.

### **What are swarms, and how do I join or start one?**

A swarm is an orchestrator and miner(s) working collaboratively to handle inference tasks. During the bootstrap script execution, you may:

* **Join an existing swarm**: Select from a list of available swarms.
* **Start a new swarm**: Enter the model name to run.

### Advanced: Can I override my node's model cache directory?

Yes, set your preferred cache directory using the `HF_HOME` variable in `~/.nesa/env/orchestrator.env`.

***

#### Additional Help/Support

If you need any additional help or support, please visit the [Nesa Discord](https://discord.gg/nesa) for community support and discussion. You can also explore additional documentation to deepen your understanding of Nesa and its features.


***
