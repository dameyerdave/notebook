# Docker

## Configure a proxy

```bash
vi ~/.docker/config.json
```

```json
{
 "proxies":
 {
   "default":
   {
     "httpProxy": "http://localhost:8888",
     "httpsProxy": "http://localhost:8888",
     "noProxy": "127.0.0.0/8"
   }
 }
}
```

## Templates

### Python

#### `Dockerfile`

```dockerfile
FROM python:3.9.6

# COPY ./requirements.txt /requirements.txt
# RUN pip install -r /requirements.txt

RUN mkdir /app
WORKDIR /app
COPY ./app /app

RUN pip install --disable-pip-version-check --upgrade pip
RUN pip install pipenv
RUN pipenv install --system --skip-lock

RUN pip install gunicorn[gevent]

RUN adduser --system user
USER user

ENTRYPOINT [ "/app/entrypoint.sh" ]
```

#### `entrypoint.sh`

```bash
#!/usr/bin/env bash
if [ ${DEBUG} -eq 1 ]; then
  python manage.py runserver 0.0.0.0:8000
else
  gunicorn --worker-class gevent --workers 8 --bind 0.0.0.0:5000 "icarus:gunicorn()" --max-requests 10000 --timeout 30 --keep-alive 5 --log-level info --log-file -
fi
```

#### `docker-compose.yml`

```yml
version: "3"
services:
  app: 
    build:
      context: .
    ports:
      - "8000:8000"
    volumes: 
      - ./app:/app
    environment:
      - PYTHONUNBUFFERED=1
      - DEBUG=1
    # command: >
    #   sh -c "python manage.py runserver 0.0.0.0:8000"
```

### Vue (Node)

#### `Dockerfile.development`

```dockerfile
FROM node:15.8.0-stretch
WORKDIR /app
COPY package*.json ./
COPY yarn.lock ./
RUN npx browserslist@latest --update-db
RUN yarn install
COPY . .
CMD yarn serve
```

#### `Dockerfile`

```dockerfile
FROM node:15.8.0-stretch as build-stage
WORKDIR /app
COPY package*.json ./
COPY yarn.lock ./
RUN npx browserslist@latest --update-db
RUN yarn install
COPY . .
RUN yarn build

FROM nginx:1.21.1 as production-stage
COPY --from=build-stage /app/dist /app

# Adjust values fom template using env vars
COPY nginx.conf /etc/nginx/nginx.conf.template
CMD /bin/bash -c "envsubst '\$NGINX_SERVER_NAME' < /etc/nginx/nginx.conf.template > /etc/nginx/nginx.conf && nginx -g 'daemon off;'"

# Run the container in a users context
RUN adduser --system user
USER user
```

## Use docker as user on linux

&rarr; found [here](https://www.digitalocean.com/community/questions/how-to-fix-docker-got-permission-denied-while-trying-to-connect-to-the-docker-daemon-socket)

```bash
sudo groupadd docker
sudo usermod -aG docker ${USER}
sudo systemctl restart docker
sudo chmod 660 /var/run/docker.sock
```

## Move docker data to a different location

&rarr; found [here](https://www.guguweb.com/2019/02/07/how-to-move-docker-data-directory-to-another-location-on-ubuntu/)

1. Stop the docker daemon

```bash
sudo service docker stop
```

2. Add a configuration file to tell the docker daemon what is the location of the data directory

```bash
vi /etc/docker/daemon.json
{ 
   "data-root": "/path/to/your/docker" 
}
```

3. Copy the current data directory to the new one

```bash
sudo rsync -aP /var/lib/docker/ "/path/to/your/docker"
```

4. Rename the old docker directory

```bash
sudo mv /var/lib/docker /var/lib/docker.old
```

5. Restart the docker daemon

```bash
sudo service docker start
```

6. Test
If everything is ok you should see no differences in using your docker containers. When you are sure that the new directory is being used correctly by docker daemon you can delete the old data directory.

```bash
sudo rm -rf /var/lib/docker.old
```

## Install Docker (CE) on Ubuntu

&rarr: found [here](https://docs.docker.com/engine/install/ubuntu/)

```bash
sudo snap remove docker
sudo apt install -y apt-transport-https ca-certificates curl gnupg lsb-release
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo \
  "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io
```

## Install Docker Compose on Ubuntu

&rarr; found [here](https://docs.docker.com/compose/install/)

```bash
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```
