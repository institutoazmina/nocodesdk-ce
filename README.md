# API Self-Hosted para Lowcoders

Um conjunto de ferramentas em forma de API para facilitar o seu dia a dia.

![API Self-Hosted para Lowcoders](nocodesdk.png)

### Assista a Live de Apresentação:

https://youtu.be/cZIJcbM2MnA

## Deploy

```yaml
---
version: "3"

services:
  nocodesdk:
    image: institutoazmina/nocodesdk:latest
    command: "php -d variables_order=EGPCS /var/www/html/artisan --workers=1 octane:start --server=swoole --host=0.0.0.0 --port=80"
    ports:
      80:${PUBLIC_PORT}
    restart: always
    env_file: .env
    environment:
        DB_PASSWORD=${MYSQL_ROOT_PASSWORD}
  redis:
    image: redis:latest
    command: ["redis-server", "--appendonly", "yes"]
  mysql:
    image: mysql
    command: --default-authentication-plugin=mysql_native_password
    restart: always
    env_file: .env
    environment:
      MYSQL_ROOT_PASSWORD: ${MYSQL_ROOT_PASSWORD}
```
