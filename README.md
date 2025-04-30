<p align="center">
<a href="https://laravel.com" target="_blank"><img src="https://raw.githubusercontent.com/marwin1991/profile-technology-icons/refs/heads/main/icons/laravel.png" width="100" alt="Laravel Logo"></a>
<a href="http://nestjs.com/" target="blank"><img src="https://raw.githubusercontent.com/marwin1991/profile-technology-icons/refs/heads/main/icons/nest_js.png" width="100" alt="Nest Logo" /></a>
<a href="https://vuejs.org/" target="blank"><img src="https://raw.githubusercontent.com/marwin1991/profile-technology-icons/refs/heads/main/icons/vue_js.png" width="100" alt="Vue Logo" /></a>
<a href="https://www.docker.com/" target="blank"><img src="https://raw.githubusercontent.com/marwin1991/profile-technology-icons/refs/heads/main/icons/docker.png" width="100" alt="Docker Logo" /></a>
</p>

# Cut URL - Proyecto completo (Laravel + NestJS + Vue)
## Description

Este repositorio contiene el proyecto completo **Cut URL**, dividido en tres partes principales:

- `api-laravel/`: API principal desarrollada en Laravel.
- `stats-nestjs/`: Servicio de estadísticas construido con NestJS.
- `stats-frontend-vue/`: Interfaz gráfica para estadísticas usando Vue.js.

Además, incluye archivos de configuración como `docker-compose.yml` y `nginx/` para correr todo con contenedores.


## ¿Cómo clonar el proyecto?

1. Clona el repositorio (incluyendo los submódulos):

```bash
git clone --recurse-submodules https://github.com/juandrescar/cut-url-project.git
cd cut-url-project
```

2. Si ya clonaste sin --recurse-submodules, puedes hacer esto:
```bash
git submodule update --init --recursive
```

### Levantar el proyecto con Docker Compose
Asegúrate de tener Docker y Docker Compose instalados en tu sistema. Luego, ejecuta los siguientes pasos desde la raíz del proyecto.

Construir e iniciar los contenedores:
```bash
docker-compose up --build
```

1. Verificar que los servicios estén corriendo:

2. Laravel (API principal) debería estar disponible en ```http://localhost:8000```

3. NestJS (API de estadísticas) debería estar disponible en ```http://localhost:3001```

4. RabbitMQ (interfaz de administración, si está habilitada) en ```http://localhost:15672```
```
Usuario: guest

Contraseña: guest
```

## Estructura del Proyecto
```bash
cut-url/
├── cut-url-api/            # Backend principal
├── stats-api/           # Servicio de estadísticas
├── url-app/     # Frontend para estadísticas
├── nginx/                  # Configuración NGINX
├── docker-compose.yml      # Orquestador de servicios
└── README.md               # Este archivo
```

## Cómo trabajar con los submódulos
Cada submódulo es un repo independiente.

Para hacer cambios en un submódulo:
```bash
cd cut-url-api
# Haces tus cambios normalmente
git checkout -b nueva-rama
git commit -am "Cambios en API"
git push origin nueva-rama
```

Luego vuelves al repo principal:

```bash
cd ..
git add cut-url-api
git commit -m "Update submodule cut-url-api to latest commit"
git push origin main
```

## Requisitos
Docker

Git

Node / PHP instalados si no usas Docker

## Configurar el contenedor Laravel:
1. Entrar en el contenedor de laravel
```bash
docker compose exec cut-url-api bash
```
2. Instalar dependencias PHP:
```bash
composer update
```
3. Copiar y renombrar el archivo de variables de entorno:
```bash
cp .env.example .env
```

4. Generar la clave de aplicación:
```bash
php artisan key:generate
```

5. Generar clave de JWT
```bash
php artisan jwt:secret
```

6. Verifica el nombre de la base de datos (no cambiar este valor):

```ini
DB_DATABASE=url_shortener
```
7. Ejecutar las migraciones:
```bash
php artisan migrate
```
8. Verificar configuración de RabbitMQ
```ini
QUEUE_CONNECTION=rabbitmq

RABBITMQ_HOST=rabbitmq
RABBITMQ_PORT=5672
RABBITMQ_USER=guest
RABBITMQ_PASSWORD=guest
RABBITMQ_VHOST=/
```

## Configurar el contenedor Nestjs
1. Entrar en el contenedor de Nestjs
```bash
docker compose exec url-stats sh
```

2. Copiar y renombrar el archivo de variables de entorno:
```bash
cp .env.example .env
```

3. Agregar secreto JWT de laravel:
```bash
JWT_SECRET=
```

## Configurar el contenedor Vue
1. Entrar en el contenedor de Vue
```bash
docker compose exec url-app sh
```

1. Copiar y renombrar el archivo de variables de entorno:
```bash
cp .env.example .env
```
