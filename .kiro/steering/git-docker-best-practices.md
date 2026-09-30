---
inclusion: auto
tags: [git, docker, github, devops, best-practices]
version: 1.0.0
author: AndresGarcia
description: Mejores prácticas para Git, GitHub y Docker en el proyecto Fresh Market
---

# 🎯 Mejores Prácticas - Git, GitHub y Docker

## 📋 INFORMACIÓN DEL PROYECTO

**Proyecto:** Fresh Market - Tienda de Alimentos Online  
**Desarrollador:** AndresGarcia  
**Tecnologías:** Node.js, React, Docker, SQLite  
**Repositorio GitHub:** (Configurar en las variables de entorno)

---

## 🔐 CONFIGURACIÓN INICIAL

### Variables de Entorno Requeridas

Para usar el MCP Server de GitHub, necesitas configurar tu token:

```bash
# Windows (CMD)
set GITHUB_TOKEN=tu_token_aquí

# Windows (PowerShell)
$env:GITHUB_TOKEN="tu_token_aquí"

# Para hacerlo permanente en Windows:
setx GITHUB_TOKEN "tu_token_aquí"
```

**Cómo obtener tu GitHub Token:**
1. Ve a: https://github.com/settings/tokens
2. Click en "Generate new token" → "Generate new token (classic)"
3. Permisos necesarios:
   - ✅ `repo` (todos los sub-permisos)
   - ✅ `workflow`
   - ✅ `read:org` (opcional)
4. Copia el token y guárdalo de forma segura

---

## 📁 ESTRUCTURA DE ARCHIVOS GIT

### .gitignore Esencial

```gitignore
# Node.js
node_modules/
npm-debug.log*
yarn-debug.log*
yarn-error.log*
package-lock.json

# Base de datos
*.db
*.sqlite
*.sqlite3
/etc/todo.db
/app/etc/todo.db

# Logs
logs/
*.log

# Environment variables
.env
.env.local
.env.*.local

# OS
.DS_Store
Thumbs.db
desktop.ini

# IDE
.vscode/
.idea/
*.swp
*.swo
*~

# Docker
docker-compose.override.yml

# Temporales
tmp/
temp/
*.tmp
```

### .dockerignore para Optimización

```dockerignore
node_modules
npm-debug.log
.git
.gitignore
README.md
.env
.env.*
.DS_Store
*.md
!package.json
!yarn.lock
.vscode
.idea
coverage
.nyc_output
*.log
```

---

## 🌿 ESTRATEGIA DE BRANCHES

### Branch Principal:
- **`main`** - Código de producción, siempre estable

### Branches de Desarrollo:
- **`develop`** - Desarrollo activo
- **`feature/nombre-feature`** - Nuevas funcionalidades
- **`bugfix/descripcion-bug`** - Corrección de bugs
- **`hotfix/descripcion-urgente`** - Fixes urgentes en producción
- **`release/vX.X.X`** - Preparación de releases

### Ejemplo de Workflow:
```bash
# Crear feature branch
git checkout -b feature/agregar-sistema-de-pago

# Trabajar y commitear
git add .
git commit -m "feat: agregar integración con stripe"

# Actualizar con cambios de develop
git checkout develop
git pull origin develop
git checkout feature/agregar-sistema-de-pago
git rebase develop

# Push y crear PR
git push -u origin feature/agregar-sistema-de-pago
```

---

## 💬 CONVENCIONES DE COMMITS

### Formato Conventional Commits:

```
tipo(scope): descripción corta

[cuerpo opcional]

[footer opcional]
```

### Tipos de Commits:

- **`feat`** - Nueva funcionalidad
  ```
  feat(carrito): agregar botón de checkout
  ```

- **`fix`** - Corrección de bug
  ```
  fix(api): corregir endpoint de productos
  ```

- **`docs`** - Cambios en documentación
  ```
  docs(readme): actualizar instrucciones de instalación
  ```

- **`style`** - Cambios de formato (no afectan código)
  ```
  style(css): mejorar espaciado en tarjetas
  ```

- **`refactor`** - Refactorización de código
  ```
  refactor(auth): simplificar lógica de autenticación
  ```

- **`test`** - Agregar o modificar tests
  ```
  test(products): agregar tests unitarios
  ```

- **`chore`** - Tareas de mantenimiento
  ```
  chore(deps): actualizar dependencias
  ```

- **`perf`** - Mejoras de performance
  ```
  perf(images): optimizar carga de imágenes
  ```

- **`ci`** - Cambios en CI/CD
  ```
  ci(docker): optimizar Dockerfile multi-stage
  ```

### Ejemplos Completos:

```bash
# Commit simple
git commit -m "feat(gallery): agregar galería de productos"

# Commit con cuerpo
git commit -m "fix(button): corregir botón añadir alimento

El botón tenía type='Enviar' en lugar de type='submit'.
Esto causaba que el formulario no se enviara correctamente.

Fixes #123"

# Commit con breaking change
git commit -m "feat(api): cambiar estructura de respuesta

BREAKING CHANGE: La API ahora retorna { data, meta } en lugar de solo data"
```

---

## 🐳 MEJORES PRÁCTICAS DOCKER

### 1. Dockerfile Optimizado

```dockerfile
# ✅ BUENA PRÁCTICA: Usar versión específica
FROM node:12.22.1-alpine3.11

# ✅ Definir WORKDIR
WORKDIR /app

# ✅ Copiar solo package files primero (cache de layers)
COPY package.json yarn.lock ./

# ✅ Instalar dependencias antes de copiar código
RUN yarn install --production --frozen-lockfile

# ✅ Copiar el resto del código
COPY . .

# ✅ Definir usuario no-root (seguridad)
USER node

# ✅ Exponer puerto
EXPOSE 3000

# ✅ Health check
HEALTHCHECK --interval=30s --timeout=3s \
  CMD node -e "require('http').get('http://localhost:3000/health', (r) => {process.exit(r.statusCode === 200 ? 0 : 1)})"

# ✅ CMD en formato exec
CMD ["node", "/app/src/index.js"]
```

### 2. Multi-Stage Build (Para producción)

```dockerfile
# Stage 1: Build
FROM node:12.22.1-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN yarn install
COPY . .

# Stage 2: Production
FROM node:12.22.1-alpine
WORKDIR /app
COPY --from=builder /app/node_modules ./node_modules
COPY --from=builder /app/src ./src
COPY --from=builder /app/package.json ./
USER node
EXPOSE 3000
CMD ["node", "src/index.js"]
```

### 3. Tags y Versionado de Imágenes

```bash
# ✅ Usar tags semánticos
docker build -t andresgarcia09/fresh-market:2.1.0 .
docker build -t andresgarcia09/fresh-market:2.1 .
docker build -t andresgarcia09/fresh-market:latest .

# ✅ Push de todas las versiones
docker push andresgarcia09/fresh-market:2.1.0
docker push andresgarcia09/fresh-market:2.1
docker push andresgarcia09/fresh-market:latest
```

### 4. Docker Compose para Desarrollo

```yaml
version: '3.8'
services:
  app:
    build: .
    ports:
      - "8080:3000"
    volumes:
      - ./src:/app/src
      - ./etc:/app/etc
    environment:
      - NODE_ENV=development
    restart: unless-stopped
```

---

## 📦 WORKFLOW DE DESPLIEGUE

### 1. Desarrollo Local

```bash
# Construir y probar localmente
docker build -t fresh-market:dev .
docker run -p 8080:3000 --name test-app fresh-market:dev

# Verificar
curl http://localhost:8080
```

### 2. Commit y Push

```bash
# Verificar cambios
git status
git diff

# Agregar archivos
git add src/static/index.html src/static/css/styles.css

# Commit con mensaje descriptivo
git commit -m "feat(ui): mejorar diseño de galería de productos

- Agregar 8 productos predefinidos con emojis
- Implementar grid responsive
- Mejorar paleta de colores (verde/naranja)
- Agregar animaciones de entrada

Desarrollado por: AndresGarcia"

# Push
git push origin develop
```

### 3. Release a Producción

```bash
# Crear tag de versión
git tag -a v2.1.0 -m "Release v2.1.0 - Fresh Market UI Improvements"
git push origin v2.1.0

# Build de producción
docker build -t andresgarcia09/fresh-market:2.1.0 .
docker build -t andresgarcia09/fresh-market:latest .

# Push a Docker Hub
docker push andresgarcia09/fresh-market:2.1.0
docker push andresgarcia09/fresh-market:latest
```

---

## 🔍 REVISIÓN DE CÓDIGO

### Checklist Antes de Commit:

- [ ] ✅ Código funciona localmente
- [ ] ✅ No hay errores en consola (F12)
- [ ] ✅ Tests pasan (si existen)
- [ ] ✅ Sin archivos de configuración sensibles (.env, tokens)
- [ ] ✅ Sin `console.log()` innecesarios
- [ ] ✅ Código comentado donde necesario
- [ ] ✅ README actualizado (si aplica)
- [ ] ✅ CHANGELOG actualizado

### Checklist Antes de Push:

- [ ] ✅ Commits siguen Conventional Commits
- [ ] ✅ Branch actualizado con main/develop
- [ ] ✅ Sin conflictos de merge
- [ ] ✅ Docker image construye correctamente
- [ ] ✅ Contenedor funciona en puerto esperado

---

## 🚀 COMANDOS ÚTILES

### Git

```bash
# Ver estado
git status

# Ver historial bonito
git log --oneline --graph --all --decorate

# Ver diferencias
git diff
git diff --staged

# Deshacer último commit (mantener cambios)
git reset --soft HEAD~1

# Deshacer cambios en archivo
git checkout -- archivo.js

# Crear y cambiar a branch
git checkout -b feature/nueva-funcionalidad

# Actualizar branch con main
git checkout main
git pull origin main
git checkout feature/nueva-funcionalidad
git rebase main

# Limpiar branches locales ya mergeadas
git branch --merged | grep -v "\*" | xargs -n 1 git branch -d
```

### Docker

```bash
# Ver imágenes
docker images

# Ver contenedores corriendo
docker ps

# Ver todos los contenedores
docker ps -a

# Ver logs en tiempo real
docker logs -f fresh-market-app

# Entrar al contenedor
docker exec -it fresh-market-app sh

# Limpiar todo (cuidado!)
docker system prune -a

# Ver uso de espacio
docker system df

# Construir sin cache
docker build --no-cache -t fresh-market .

# Stop y remove
docker stop fresh-market-app && docker rm fresh-market-app
```

---

## 🔒 SEGURIDAD

### ❌ NUNCA Subir a Git:

- Tokens de API
- Passwords
- Archivos `.env`
- Claves SSH privadas
- Certificados SSL privados
- Base de datos con datos reales

### ✅ Usar Variables de Entorno:

```javascript
// ❌ MAL
const apiKey = "sk_live_123456789";

// ✅ BIEN
const apiKey = process.env.API_KEY;
```

### Escanear Secretos:

```bash
# Instalar git-secrets
git secrets --install
git secrets --register-aws
```

---

## 📊 VERSIONADO SEMÁNTICO

Formato: `MAJOR.MINOR.PATCH`

### MAJOR (1.0.0 → 2.0.0)
- Cambios incompatibles con versiones anteriores
- Breaking changes en la API

### MINOR (2.0.0 → 2.1.0)
- Nuevas funcionalidades compatibles
- Mejoras significativas
- Nuevas features

### PATCH (2.1.0 → 2.1.1)
- Bug fixes
- Correcciones menores
- Mejoras de performance

### Ejemplo del Proyecto:
- **v1.0.0** - TODO list original
- **v2.0.0** - Fresh Market con nuevo UI (breaking change visual)
- **v2.1.0** - Corrección botón añadir (bug fix importante)
- **v2.2.0** - (Futuro) Agregar sistema de categorías

---

## 📝 README.md Esencial

Tu README debe incluir:

```markdown
# Fresh Market 🛒

Tienda online de alimentos frescos y naturales

## 🚀 Inicio Rápido

### Prerequisitos
- Docker 20.x+
- Node.js 12.x (para desarrollo local)

### Instalación

1. Clonar repo:
   ```bash
   git clone https://github.com/andresgarcia09/fresh-market.git
   cd fresh-market
   ```

2. Construir imagen:
   ```bash
   docker build -t fresh-market .
   ```

3. Ejecutar:
   ```bash
   docker run -p 8080:3000 fresh-market
   ```

4. Abrir: http://localhost:8080

## 🛠️ Tecnologías

- Node.js + Express
- React
- SQLite
- Docker
- Bootstrap

## 👨‍💻 Autor

**AndresGarcia** - Desarrollador Full Stack

## 📄 Licencia

MIT License
```

---

## 🎯 WORKFLOW COMPLETO - EJEMPLO PRÁCTICO

```bash
# 1. Iniciar nueva feature
git checkout develop
git pull origin develop
git checkout -b feature/sistema-de-busqueda

# 2. Desarrollar
# ... hacer cambios en el código ...

# 3. Probar localmente
docker build -t fresh-market:test .
docker run -p 8080:3000 fresh-market:test

# 4. Commit
git add src/static/js/search.js
git commit -m "feat(search): agregar búsqueda de productos

- Implementar input de búsqueda
- Filtrar productos por nombre
- Animación de resultados"

# 5. Push y crear PR
git push -u origin feature/sistema-de-busqueda

# 6. Después del merge a develop
git checkout develop
git pull origin develop

# 7. Release
git checkout main
git merge develop
git tag -a v2.2.0 -m "Release v2.2.0"
git push origin main --tags

# 8. Build y push Docker
docker build -t andresgarcia09/fresh-market:2.2.0 .
docker push andresgarcia09/fresh-market:2.2.0
```

---

## 📚 RECURSOS ÚTILES

### Documentación:
- [Git Documentation](https://git-scm.com/doc)
- [Docker Best Practices](https://docs.docker.com/develop/dev-best-practices/)
- [Conventional Commits](https://www.conventionalcommits.org/)
- [Semantic Versioning](https://semver.org/)

### Tools:
- [GitHub CLI](https://cli.github.com/)
- [Docker Desktop](https://www.docker.com/products/docker-desktop/)
- [GitKraken](https://www.gitkraken.com/) (GUI para Git)

---

## ✅ CHECKLIST DIARIA

Antes de terminar tu día de trabajo:

- [ ] Todos los cambios committed
- [ ] Branch pusheado a GitHub
- [ ] PR creada (si aplica)
- [ ] Docker image funciona
- [ ] Documentación actualizada
- [ ] No hay archivos sensibles en el repo

---

**Última actualización:** 2024  
**Mantenido por:** AndresGarcia  
**Versión del documento:** 1.0.0
