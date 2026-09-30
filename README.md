# 🛒 Fresh Market - Tienda de Alimentos Online

<div align="center">

![Fresh Market](https://img.shields.io/badge/Fresh%20Market-2.1.0-green?style=for-the-badge&logo=react)
![Docker](https://img.shields.io/badge/Docker-Ready-blue?style=for-the-badge&logo=docker)
![Node.js](https://img.shields.io/badge/Node.js-12.22.1-green?style=for-the-badge&logo=node.js)
![License](https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge)

**Tienda online profesional de alimentos frescos y naturales**

[Características](#-características) • [Inicio Rápido](#-inicio-rápido) • [Documentación](#-documentación)

</div>

---

## 📝 Descripción

Fresh Market es una aplicación web moderna para la gestión de compras de alimentos frescos. Desarrollada con Node.js, React y Docker, ofrece una experiencia de usuario intuitiva y profesional.

**Versión:** 2.1.0 | **Desarrollado por:** AndresGarcia

---

## 🌟 Características

✅ **Galería de Productos** - 8 productos con precios  
✅ **Carrito de Compras** - Agregar, marcar como comprado, eliminar  
✅ **Diseño Responsive** - Móvil, tablet y desktop  
✅ **Dockerizado** - Despliegue con un comando  
✅ **API REST** - Backend completo con Express + SQLite

---

## 🚀 Inicio Rápido

### Usando Docker (Recomendado)

```bash
# 1. Clonar el repositorio
git clone https://github.com/Andres-0903/Tienda_Alimentos_Docker.git
cd Tienda_Alimentos_Docker

# 2. Construir imagen Docker
docker build -t fresh-market .

# 3. Ejecutar contenedor
docker run -d -p 8080:3000 --name fresh-market-app fresh-market

# 4. Abrir en navegador
# http://localhost:8080
```

### Desarrollo Local

```bash
# Instalar dependencias
yarn install

# Ejecutar en modo desarrollo
yarn dev

# Abrir: http://localhost:3000
```

---

## 🛠️ Tecnologías

- **Backend:** Node.js + Express + SQLite
- **Frontend:** React + Bootstrap + CSS3
- **DevOps:** Docker + Alpine Linux
- **Styling:** CSS Variables + Flexbox/Grid

---

## 📂 Estructura del Proyecto

```
fresh-market/
├── src/
│   ├── static/           # Frontend
│   │   ├── css/         # Estilos
│   │   ├── js/          # React app
│   │   └── index.html   # HTML principal
│   ├── persistence/      # Base de datos
│   ├── routes/          # API endpoints
│   └── index.js         # Servidor Express
├── docs/                # Documentación detallada
├── spec/                # Tests
├── etc/                 # Base de datos SQLite
├── .kiro/              # Configuración Kiro/MCP
├── Dockerfile          # Imagen Docker
├── package.json        # Dependencias
└── README.md          # Este archivo
```

---

## 📚 Documentación

Documentación detallada en la carpeta `docs/`:

- **[INICIO RÁPIDO](docs/README_QUICK_START.md)** - Guía de 3 pasos
- **[INSTRUCCIONES DEPLOY](docs/INSTRUCCIONES_DEPLOY.md)** - Despliegue completo
- **[CHANGELOG](docs/CHANGELOG_MEJORAS.md)** - Historial de cambios
- **[RESUMEN VISUAL](docs/RESUMEN_CAMBIOS.md)** - Antes/Después
- **[GUÍA GITHUB](docs/GUIA_GITHUB_SETUP.md)** - Configuración Git/MCP
- **[BUG FIXES](docs/PROBLEMA_RESUELTO.md)** - Correcciones aplicadas

---

## 🔌 API Endpoints

| Método | Endpoint | Descripción |
|--------|----------|-------------|
| GET | `/items` | Obtener todos los productos |
| POST | `/items` | Agregar un producto |
| PUT | `/items/:id` | Actualizar producto |
| DELETE | `/items/:id` | Eliminar producto |

Ver documentación completa en `docs/`

---

## 🐳 Comandos Docker Esenciales

```bash
# Construir
docker build -t fresh-market .

# Ejecutar
docker run -d -p 8080:3000 --name fresh-market-app fresh-market

# Ver logs
docker logs -f fresh-market-app

# Detener y limpiar
docker stop fresh-market-app && docker rm fresh-market-app
```

---

## 👨‍💻 Desarrollo

```bash
# Instalar
yarn install

# Desarrollo
yarn dev

# Tests
yarn test

# Formatear código
yarn prettify
```

---

## 👨‍💻 Autor

**AndresGarcia**

- GitHub: [@Andres-0903](https://github.com/Andres-0903)
- Repositorio: [Tienda_Alimentos_Docker](https://github.com/Andres-0903/Tienda_Alimentos_Docker)

---

## 📄 Licencia

Este proyecto está bajo la Licencia MIT.

---

## 🙏 Soporte

¿Problemas o preguntas? Revisa la [documentación en docs/](docs/) o crea un [Issue](https://github.com/Andres-0903/Tienda_Alimentos_Docker/issues).

---

<div align="center">

**Hecho con ❤️ por AndresGarcia**

⭐ Si te gustó el proyecto, dale una estrella en GitHub

</div>
