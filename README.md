# How to install and setup RustDesk server using docker

## docker-rustdek-server-setup-guide

This guide is for Docker RustDesk setup instructions.

1. Create work directories:
```bash
sudo mkdir -p /opt/rustdesk
```

2. Docker command for HBBS
```bash
sudo docker run -d \
  -p 21115:21115/tcp \
  -p 21116:21116/tcp \
  -p 21116:21116/udp \
  -v /opt/rustdesk:/root \
  --name rustdesk-hbbs \
  rustdesk/rustdesk-server hbbs
``` 

3. Docker command for HBBR
```bash
sudo docker run -d \
  -p 21117:21117/tcp \
  -v /opt/rustdesk:/root \
  --name rustdesk-hbbr \
  rustdesk/rustdesk-server hbbr
```

3. UFW allow rules (only minimal required)
```bash
sudo ufw allow 21115/tcp
sudo ufw allow 21116/tcp
sudo ufw allow 21116/udp
sudo ufw allow 21117/tcp
```

3. After running these command you can find PUB key in directory selected in this case it is /opt/rustdesk
Copy id and save it to use later for RustDesk clients.
```bash
cat /opt/rustdesk/id_ed01.pub
```

4. You will have to add you server IP information to RustDesk client
ID server
```bash
100.00.00.01:21116
```
Relay server
```bash
100.00.00.01:21117
```
