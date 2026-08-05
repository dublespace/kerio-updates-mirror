<div align="center">

# 🔄 Kerio Updates Mirror

Kerio Updates Mirror — Portainer Stack
Готовый стек для автоматического развёртывания зеркала обновлений Kerio через веб-интерфейс Portainer.
🚀 Инструкция по установке в Portainer
Развёртывание Стека:
Перейдите в Portainer -> Stacks -> нажмите + Add stack.
Введите имя: `kmc-kerio`.
В блоке Build method выберите Repository.
Заполните поля:
Repository URL: `https://github.com/dublespace/kmc-kerio`
Repository reference: `refs/heads/main`
Compose path: `docker-compose.yml`
Нажмите Deploy the stack.
---
cd /root/docker

git clone https://github.com/dublespace/kerio-updates-mirror.git

cd kerio-updates-mirror

# 1. Сборка Nginx
DOCKER_BUILDKIT=1 docker build -t kum_nginx:v1.31.3 ./_nginx

# 2. Сборка Mirror
DOCKER_BUILDKIT=1 docker build -t kum_mirror:v3.0.4 ./_mirror

# 3. Сборка Xray
DOCKER_BUILDKIT=1 docker build -t kum_xray:v26.3.27 ./_xray

# 4. Сборка Tor
DOCKER_BUILDKIT=1 docker build -t kum_tor:v0.4.9.11 ./_tor

chmod +x /root/docker/kerio-updates-mirror/_tor/start.sh

chmod -R 644 /root/docker/kerio-updates-mirror/_tor/*

chmod +x /root/docker/kerio-updates-mirror/_tor/start.sh
