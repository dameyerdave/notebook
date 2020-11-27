# Docker

## Use docker as user on linux

&rarr; found [here](https://www.digitalocean.com/community/questions/how-to-fix-docker-got-permission-denied-while-trying-to-connect-to-the-docker-daemon-socket)

```bash
sudo groupadd docker
sudo usermod -aG docker ${USER}
sudo systemctl restart docker
sudo chmod 660 /var/run/docker.sock
```