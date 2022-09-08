# actions-self-hosted-runners

[![CI](https://github.com/peaceiris/actions-self-hosted-runners/actions/workflows/ci.yml/badge.svg?event=push)](https://github.com/peaceiris/actions-self-hosted-runners/actions/workflows/ci.yml)

GitHub Actions self-hosted runner on VirtualBox with Vagrant.

- [actions/runner](https://github.com/actions/runner): The Runner for GitHub Actions
- [actions/virtual-environments](https://github.com/actions/virtual-environments): GitHub Actions virtual environments

## Getting Started

```sh
# clone and start vm
git clone https://github.com/peaceiris/actions-self-hosted-runners.git
cd ./actions-self-hosted-runners/images/ubuntu-22.04
vim .env
make up
# enter vm and become root
vagrant ssh
sudo bash
cd ~/actions-runner
# setup actions runner
export RUNNER_ALLOW_RUNASROOT=1
./config.sh --url https://github.com/[owner]/[repo] --token [token]
nohup ./run.sh &
```

We're running as root so that GitHub Actions Runner can clean up old Docker files, otherwise [there are permission errors](https://github.com/actions/runner/issues/434).

Create `.env` file as follows, find GitHub Actions Runner versions here:

https://github.com/actions/runner/releases

```rb
GHA_RUNNER_VERSION = 'x.xxx.x'
VB_CPUS = '4'
VB_MEMORY = '8192'
VB_DISK_SIZE = '30GB'
```
