# Install Docker Compose on Amazon Linux 2

## Step 1. Download the latest Docker Compose version.

```
wget https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)
```

## Step 2. Move the Docker Compose file into the system binaries.

```
sudo mv docker-compose-$(uname -s)-$(uname -m) /usr/local/bin/docker-compose
```

## Step 3. Apply the right permissions.

```
sudo chmod -v +x /usr/local/bin/docker-compose
```

## Step 4. Verify installation.

```
docker-compose version
```