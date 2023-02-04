# lamina1-node
Lamina1 containerized node setup and related infrastructure stuff

Official doc: https://docs.lamina1.network/docs/userguide/#running-a-lamina1-node

## Prerequisites
* Docker
* git

## TESTNET node setup
1. Clone repo git clone
   ```
   git clone https://github.com/wdstorer/lamina1-node.git
   ```
2. cd into the project folder 
   ```
   cd lamina1-node
   ```
5. Build the container
   ```
   docker build -f docker/Dockerfile -t lamina1-node:latest .
   ```
4. Run the lamina1 node in the background, persist data in a volume, and restart container when the computer is rebooted
   ```
   docker run -d --restart unless-stopped \
                 --name lamina1-node-testnet \
                 --mount source=lamina1-testnet-data,target=/data \
                 lamina1-node:latest --config-file configs/testnet/default.json --data-dir /data
   ```
5. Confirm that the container is running in the background 
   ```
   docker ps
   ```
6. Tail the logs until you start seeing output (note it may take several minutes for any output to show up) `Ctrl+c` to stop tailing the log
   ```
   docker logs -f lamina1-node-testnet
   ```
7. Run check-bootstrap.sh to confirm that API is up and the chains are synced (It will take awhile for the chains to sync from scratch)
   ```
   docker exec -it lamina1-node-testnet ./check-bootstrap.sh
   ```

## Useful commands
```
# stop the container
docker stop lamina1-node-testnet

# delete the container
docker rm lamina1-node-testnet

# delete the image
docker rmi lamina1-node-testnet

# delete persistent storage
docker volume rm lamina1-testnet-data
```
