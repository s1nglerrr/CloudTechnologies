# Установка Docker на Windows и запуск майнкрафт 1.20.1 сервера в контейнере

## 1. Установка Docker на Windows

### 1.1. Установка WSL 2

Docker использует WSL 2 для работы с Linux контейнерами. Открыть **PowerShell или командную строку** от имени администратора и выполнить:

```powershell
wsl --install
```

> **После выполнения команды потребуется перезагрузка компьютера.**

### 1.2. Скачивание Docker Desktop

Переходим на сайт:  
[https://www.docker.com/products/docker-desktop/](https://www.docker.com/products/docker-desktop/)

Я выбрал **Download for Windows – AMD64**.

После установки докера, запускаем его. При первом запуске соглашаемся с условиями использования и создаем аккаунт (необязательно).

## 2. Создание Dockerfile для майнкрафт сервера

Теперь создадим папку для нашего сервера и внутри неё - `docker-compose.yml`.

### 2.1. Содержимое Dockerfile

```dockerfile
version: "3.8"

services:
  minecraft-java:
    image: itzg/minecraft-server
    container_name: mc-java-server
    ports:
      - "25565:25565"
    environment:
      EULA: "TRUE"
      VERSION: "1.20.1"
      TYPE: "PAPER"
      MEMORY: "2G"
    volumes:
      - ./minecraft-data:/data
    restart: unless-stopped
```
### 2.3. Сборка образа

Далее нужно открыть терминал в папке с `docker-compose.yml` и выполнить:

```bash
docker build -t minecraft-server .
```

### 2.4. Запуск контейнера

Для начала запускаем докер десктоп, а затем поднимаем контейнер:
```bash
docker-compose up -d
```
- `up` — запустить
- `-d` — запуск в фоне

Мы запустили сервер. Заходим в майнкрафт и заходим на сервер по адресу `localhost:25565`.

### Скриншоты этапов установки и запуска:

![photo_2026-04-10_08-54-58](https://github.com/user-attachments/assets/d6e6dae2-cbb7-4e8c-8a49-c33780298ad1)
![photo_2026-04-10_08-55-03](https://github.com/user-attachments/assets/a77d9be2-3253-4d34-a033-dffc2a811f60)
![photo_2026-04-10_08-54-51](https://github.com/user-attachments/assets/7ec32c93-ecda-441a-8107-9aaa25de1f59)
![photo_2026-04-10_08-54-56](https://github.com/user-attachments/assets/469e3b74-e50e-4164-a339-5d4d8eb6a01e)
![photo_2026-04-10_08-54-46](https://github.com/user-attachments/assets/dbf49ef0-0ced-4f34-a016-84296c81c9e5)
![photo_2026-04-10_08-54-48](https://github.com/user-attachments/assets/1272febc-d309-4afb-a21f-0d57a8c77fb0)
