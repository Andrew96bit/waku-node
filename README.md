### Waku Node Setup Guide

#### Server Preparation:

```bash
sudo apt-get update && sudo apt-get upgrade -y && sudo apt-get install make curl build-essential unzip lz4 gcc git jq -y
```

#### Install Docker and Docker Compose:

1. Install dependencies:
   
   ```bash
   sudo apt install -y ca-certificates curl gnupg lsb-release
   ```

2. Add Docker’s official GPG key:

   ```bash
   curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
   ```

3. Set up the stable repository:

   ```bash
   echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
   ```

4. Install Docker Engine and Docker Compose:

   ```bash
   sudo apt update && sudo apt install -y docker-ce docker-ce-cli containerd.io
   sudo usermod -aG docker $USER
   newgrp docker
   ```

5. Download and install Docker Compose:

   ```bash
   sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
   sudo chmod +x /usr/local/bin/docker-compose
   ```

#### Install Waku Node:

1. Clone the repository:

   ```bash
   git clone https://github.com/waku-org/nwaku-compose
   ```

2. Navigate to the repository folder:

   ```bash
   cd nwaku-compose
   ```

3. Copy the example environment file:

   ```bash
   cp .env.example .env
   ```

4. Open the `.env` file in a text editor and modify the following variables:

   ```bash
   nano .env
   ```

   - `ETH_CLIENT_ADDRESS`: RPC link of a node provider (Alchemy or Infura in the Sepolia network)
   - `ETH_TESTNET_KEY`: Private key from MetaMask
   - `RLN_RELAY_CRED_PASSWORD`: Set a password of your choice

#### Register the Node in the Network:

```bash
./register_rln.sh
```

#### Start the Node:

```bash
docker-compose up -d
```

#### Check Logs:

```bash
docker-compose logs -f nwaku
```

Grafana can be accessed here (replace with relevant link).

---

### Update Instructions:

1. Navigate to the Waku repository folder:

   ```bash
   cd nwaku-compose
   ```

2. Stop the current instance:

   ```bash
   docker-compose down
   ```

3. Pull the latest changes:

   ```bash
   git pull
   ```

4. Pull the latest Docker images:

   ```bash
   docker-compose pull
   ```

5. Start the updated node:

   ```bash
   docker-compose up -d
   ```

### Grafana Node monitoring

```bash
   http://YourServerIP:3000/d/yns_4vFVk/nwaku-monitoring?orgId=1
   ```
