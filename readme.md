# Run RL Swarm (Testnet) Node

RL Swarm is a fully open-source framework developed by GensynAI for building reinforcement learning (RL) training swarms over the internet. This guide walks you through setting up an RL Swarm node and a web UI dashboard to monitor swarm activity.

## Hardware Requirements
- **CPU**: Minimum 16GB RAM (more RAM recommended for larger models or datasets).

**OR**

- **GPU (Optional)**: Supported CUDA devices for enhanced performance:
  - RTX 3090
  - RTX 4090
  - A100
  - H100
  > GPUs with >= 24GB vRAM are recommended.

- **Note**: You can run the node without a GPU using CPU-only mode.

---

## Install Dependencies

1. Update and upgrade system packages:
   ```
   sudo apt-get update && sudo apt-get upgrade -y
   ```

2. Install required packages:
   ```
   sudo apt install screen curl iptables build-essential git wget lz4 jq make gcc nano automake autoconf tmux htop nvme-cli libgbm1 pkg-config libssl-dev libleveldb-dev tar clang bsdmainutils ncdu unzip libleveldb-dev -y
   ```

3. Install Python and related tools:
   ```
   sudo apt-get install python3 python3-pip python3-venv python3-dev -y
   ```

4. Install Node.js and Yarn:
   - Add the Node.js repository and install Node.js:
     ```
     sudo apt-get update
     curl -fsSL https://deb.nodesource.com/setup_22.x | sudo -E bash -
     sudo apt-get install -y nodejs
     node -v
     ```
   - Install Yarn globally:
     ```
     sudo npm install -g yarn
     yarn -v
     ```

5. Install Yarn locally:
   ```
   curl -o- -L https://yarnpkg.com/install.sh | bash
   export PATH="$HOME/.yarn/bin:$HOME/.config/yarn/global/node_modules/.bin:$PATH"
   source ~/.bashrc
   ```

---

## After Installing Dependencies

1. Clone the RL Swarm repository:
   ```
   cd $HOME
   git clone https://github.com/gensyn-ai/rl-swarm/
   cd rl-swarm
   ```

2. Set up a Python virtual environment:
   ```
   python3 -m venv .venv
   source .venv/bin/activate
   ```

3. Configure the `modal-login` module:
   ```
   cd modal-login
   yarn install
   yarn upgrade && yarn add next@latest && yarn add viem@latest
   ```

4. Start your node:
   ```
   cd rl-swarm
   ./run_rl_swarm.sh
   ```

---

## Troubleshooting Steps

### PS1 Error
If you see a PS1 error, follow these steps:
1. Stop your node.
2. Before restarting your node, run this command:
   ```
   sed -i '1i # ~/.bashrc: executed by bash(1) for non-login shells.\n\n# If not running interactively, don'\''t do anything\ncase $- in\n    *i*) ;;\n    *) return;;\nesac\n' ~/.bashrc
   ```
3. Restart your node:
   ```
   ./run_rl_swarm.sh
   ```

---

## For CPU Users Only

1. Open the configuration file:
   ```
   nano ~/rl-swarm/hivemind_exp/configs/gpu/grpo-qwen-2.5-0.5b-deepseek-r1.yaml
   ```

2. Edit the `max_steps` parameter:
   - Locate the line: `max_steps: 20 # Original 450`
   - Change it to:
     ```
     max_steps: 5
     ```
