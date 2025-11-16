# 🚀 Stack PHP 8.4 + Nginx + MySQL + Xdebug (Docker)

Este entorno incluye:

- PHP **8.4 FPM Alpine**
- Xdebug **3.3+**
- Nginx stable
- MySQL **8.0.41**
- Composer
- Node + NPM
- Hot reload listo para trabajar con Laravel o cualquier API PHP

---

## 1. Requisitos

- Docker 24+
- Docker Compose v2
- Carpeta del proyecto mapeada en: `${HOME}/${DIRHOME}/api`

---

## 2. Iniciar el entorno

```bash
docker compose up -d --build
```

---

## 3. Verificar MySQL
```bash
docker exec -it {APP_NAME}_mysql mysql -u root -p
```

---

## 4. Verificar versión de PHP (8.4)

```bash
docker exec -it {APP_NAME}_phpfpm php -v
```

---

## 5. Verificar Xdebug

Activar log:
```bash
docker exec -it {APP_NAME}_phpfpm tail -f /tmp/xdebug.log
```

VSCode launch.json:
```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Listen for Xdebug",
      "type": "php",
      "request": "launch",
      "port": 9003,
      "pathMappings": {
        "/var/www/app": "${workspaceFolder}"
      }
    }
  ]
}
```

---

## 6. Instalar dependencias del proyecto

```bash
docker exec -it {APP_NAME}_phpfpm composer install
```

Para proyectos laravel:
```bash
docker exec -it {APP_NAME}_phpfpm php artisan key:generate
```

---

## 7. Reiniciar el stack
```bash
docker compose restart
```

---

## 8. Probar funcionamiento

Crear public/index.php:
```php
<?php
phpinfo();
```

Ir a http://localhost:${WEB_PORT}


---

## 7. 
```bash

```

---

## 7. 
```bash

```






