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
