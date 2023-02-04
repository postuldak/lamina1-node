# lamina1-node
Lamina1 node setup and related infrastructure stuff

Prerequisites
* Docker

TESTNET node setup
# Clone repo git clone...
# cd into project folder
# Build container: 
  `docker build -f docker/Dockerfile -t lamina1-node:latest .`
# Run container, creating a docker volume to persist data and restarting on reboot
# Run the lamina1 node in the background, persist data in a volume, and restart container when the computer is rebooted
  `docker run -d --restart unless-stopped --name lamina1-node-testnet --mount source=data,target=/data lamina1-node:latest --config-file configs/testnet/default.json --data-dir /data`
# Confirm that the container is running in the background 
  `docker ps`
# Check the logs
  `docker logs lamina1-node-testnet`
# Run check-bootstrap.sh
  `docker exec -it lamina1-node-testnet ./check-bootstrap.sh`
