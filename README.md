# rchain-launcher
Script for launching an rchain testnet node on a docker image.

This script has variables in it, requirements:
1. Docker installed (see below)
2. Docker network created (see below)
3. Have an RChain key pair created (see below)

## For Ubuntu 18.04:
1. Install Docker
- `sudo apt install docker.io`
2. Add your current user to the docker group
`sudo gpasswd -a $USER docker`
3. Log out and log back in
4. Create your docker network
`docker network create rnode-net`
5. Pull the latest docker image
`docker pull rchain/rnode:latest`
6. Get your docker key (see below), find the bootstrap node, and get the links for the bonds.txt and wallets.txt files.
7. Change variables for private key, network, and bootstrap node in the rchain_docker.sh file
`nano rchain_docker.sh`
8. Run

### Generating RChain Keys
To get your rnode key generated, start rnode in standalone mode (see below) - let it run for 1 minute, and then stop it. Go to your rnode/genesis folder.

There will be 5 .sk files in there. The title of each file is the pub key and the contents of each file are the priv key.

#### To start your node in standalone mode:
1. First create a local rnode directory
`mkdir ~/rnode`

2. Pull the rnode latest docker image
`docker pull rchain/rnode:latest`

3. Then run the docker command
`docker run -u root -it --network rnode-net --name rnode-standalone -v "$HOME/rnode":/var/lib/rnode rchain/rnode:latest run --standalone`

4. After it runs for 1 minute, stop the docker using control-c to break

5. Go to your ~/rnode/genesis directory and run `ls -la` and then `cat *.sk` each of those files contains a key pair. The name of the file is the public key and the contents are the private key. You will need both - save them somewhere safe and private.

#### Additional documentation on running rnode:
https://rchain.atlassian.net/wiki/spaces/CORE/pages/428376065/User+guide+for+running+RNode
