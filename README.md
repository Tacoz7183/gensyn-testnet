# gensyn-testnet -Tacoz7183
# Run RL Swarm (Testnet) Node
RL Swarm is a fully open-source framework developed by GensynAI for building reinforcement learning (RL) training swarms over the internet. This guide walks you through setting up an RL Swarm node and a web UI dashboard to monitor swarm activity.

## Hardware Requirements
- CPU: Minimum 16GB RAM (more RAM recommended for larger models or datasets).

OR

- GPU (Optional): Supported CUDA devices for enhanced performance:
    - RTX 3090
    - RTX 4090
    - A100
    - H100
    > I recommend GPUs with >=24GB vRAM.
-  **Note**: You can run the node without a GPU using CPU-only mode.

Install Dependencies

1- sudo apt-get update && sudo apt-get upgrade -y

2- sudo apt install screen curl iptables build-essential git wget lz4 jq make gcc nano automake autoconf tmux htop nvme-cli libgbm1 pkg-config libssl-dev libleveldb-dev tar clang bsdmainutils ncdu unzip libleveldb-dev  -y

3- sudo apt-get install python3 python3-pip python3-venv python3-dev -y

4- sudo apt-get update
curl -fsSL https://deb.nodesource.com/setup_22.x | sudo -E bash -
sudo apt-get install -y nodejs
node -v
sudo npm install -g yarn
yarn -v

5-a)- curl -o- -L https://yarnpkg.com/install.sh | bash
  b)- export PATH="$HOME/.yarn/bin:$HOME/.config/yarn/global/node_modules/.bin:$PATH"
  c)- source ~/.bashrc

After installing depencies

0)- cd $home

1- git clone https://github.com/gensyn-ai/rl-swarm/

2- cd rl-swarm

3- python3 -m venv .venv
source .venv/bin/activate

4-a)- cd modal-login
  b)- yarn install

  c)- yarn upgrade && yarn add next@latest && yarn add viem@latest
  d)- cd ..

5-Now Start your node- ./run_rl_swarm.sh





Troubleshooting steps 

If You See PS1 error  -- Solution- stop your node AND before restarting your node  paste this command then Enter 

1-  sed -i '1i # ~/.bashrc: executed by bash(1) for non-login shells.\n\n# If not running interactively, don'\''t do anything\ncase $- in\n    *i*) ;;\n    *) return;;\nesac\n' ~/.bashrc

2- ./run_rl_swarm.sh

For CPU users only 

1- nano ~/rl-swarm/hivemind_exp/configs/gpu/grpo-qwen-2.5-0.5b-deepseek-r1.yaml

2- (max_steps: 20 # Original 450) go to this line and edit 20 to max_steps: 5

