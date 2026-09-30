# 🚀 INSTRUCCIONES DE DESPLIEGUE - Fresh Market

## 📋 Prerequisitos

Antes de empezar, asegúrate de tener instalado:

- **Docker** (versión 20.x o superior)
- **Terminal** con acceso a comandos Docker
- **Editor de texto** (opcional, para verificar cambios)

---

## 🔨 PASO 1: Verificar los Archivos Modificados

Los siguientes archivos han sido modificados:

```
app/
├── src/
│   └── static/
│       ├── index.html          ✅ MODIFICADO
│       └── css/
│           └── styles.css      ✅ MODIFICADO
├── CHANGELOG_MEJORAS.md        ✅ NUEVO
└── INSTRUCCIONES_DEPLOY.md     ✅ NUEVO (este archivo)
```

**¡IMPORTANTE!** Los archivos del backend NO han sido modificados:
- `src/index.js` ✅ Sin cambios
- `src/persistence/` ✅ Sin cambios
- `src/routes/` ✅ Sin cambios
- `Dockerfile` ✅ Sin cambios
- `package.json` ✅ Sin cambios

---

## 🐳 PASO 2: Construir la Imagen Docker

Abre tu terminal y navega a la carpeta del proyecto:

```bash
cd "C:\Users\Andres\Desktop\Curso Docker Udemy\app"
```

### Opción A: Construir sin nombre de usuario (local)

```bash
docker build -t fresh-market:v2.0 .
```

### Opción B: Construir con tu usuario de Docker Hub

```bash
docker build -t andresgarcia09/fresh-market:v2.0 .
```

**Tiempo estimado:** 2-5 minutos (dependiendo de tu conexión)

### Verificar que la imagen se creó correctamente:

```bash
docker images
```

Deberías ver algo como:

```
REPOSITORY                        TAG       IMAGE ID       CREATED          SIZE
andresgarcia09/fresh-market       v2.0      abc123def456   2 minutes ago    150MB
```

---

## ▶️ PASO 3: Ejecutar el Contenedor

### Opción A: Ejecutar con nombre de usuario

```bash
docker run -d -p 8080:3000 --name fresh-market-app andresgarcia09/fresh-market:v2.0
```

### Opción B: Ejecutar sin nombre de usuario (local)

```bash
docker run -d -p 8080:3000 --name fresh-market-app fresh-market:v2.0
```

### Explicación de los parámetros:

- `-d` → Ejecuta el contenedor en segundo plano (detached)
- `-p 8080:3000` → Mapea el puerto 3000 del contenedor al puerto 8080 de tu máquina
- `--name fresh-market-app` → Asigna un nombre al contenedor para fácil identificación
- `andresgarcia09/fresh-market:v2.0` → Nombre de la imagen a ejecutar

---

## 🌐 PASO 4: Verificar que Funciona

### 1. Verificar que el contenedor está corriendo:

```bash
docker ps
```

Deberías ver:

```
CONTAINER ID   IMAGE                                  STATUS         PORTS
abc123def456   andresgarcia09/fresh-market:v2.0      Up 10 seconds  0.0.0.0:8080->3000/tcp
```

### 2. Abrir el navegador:

```
http://localhost:8080
```

**¡Deberías ver tu nueva tienda Fresh Market!** 🎉

---

## 🔍 PASO 5: Verificar las Mejoras Visuales

### Checklist de elementos a verificar:

- [ ] ✅ **Header/Navbar** con logo "Fresh Market" y enlaces
- [ ] ✅ **Hero banner** verde con título "Alimentos Frescos y Naturales"
- [ ] ✅ **Galería de 8 productos** con emojis, precios y botones
- [ ] ✅ **Sección de carrito** funcionando (agregar/eliminar items)
- [ ] ✅ **Footer** con información de contacto y créditos "Desarrollado por AndresGarcia"
- [ ] ✅ **Responsive** (prueba redimensionar la ventana)
- [ ] ✅ **Animaciones** suaves al hacer hover en productos
- [ ] ✅ **Scroll suave** al hacer click en enlaces de navegación

### Probar funcionalidad:

1. **Click en un botón "Agregar"** de la galería → Producto aparece en el carrito
2. **Escribir manualmente** un producto en el input → Añadirlo con el botón
3. **Marcar checkbox** de un producto → Se tacha (producto comprado)
4. **Click en el icono de basura** → Elimina el producto

---

## 🛑 COMANDOS ÚTILES

### Ver logs del contenedor:

```bash
docker logs fresh-market-app
```

### Detener el contenedor:

```bash
docker stop fresh-market-app
```

### Iniciar el contenedor (si está detenido):

```bash
docker start fresh-market-app
```

### Reiniciar el contenedor:

```bash
docker restart fresh-market-app
```

### Eliminar el contenedor:

```bash
docker stop fresh-market-app
docker rm fresh-market-app
```

### Eliminar la imagen:

```bash
docker rmi andresgarcia09/fresh-market:v2.0
```

---

## 📤 PASO 6: Publicar en Docker Hub (Opcional)

Si quieres compartir tu imagen en Docker Hub:

### 1. Login en Docker Hub:

```bash
docker login
```

Te pedirá tu usuario y contraseña de Docker Hub.

### 2. Push de la imagen:

```bash
docker push andresgarcia09/fresh-market:v2.0
```

### 3. Verificar en Docker Hub:

Visita: `https://hub.docker.com/r/andresgarcia09/fresh-market`

---

## 🔄 PASO 7: Actualizar con Nuevos Cambios

Si haces cambios en el HTML o CSS:

```bash
# 1. Detener y eliminar el contenedor actual
docker stop fresh-market-app
docker rm fresh-market-app

# 2. Reconstruir la imagen con una nueva versión
docker build -t andresgarcia09/fresh-market:v2.1 .

# 3. Ejecutar el nuevo contenedor
docker run -d -p 8080:3000 --name fresh-market-app andresgarcia09/fresh-market:v2.1
```

---

## 🐛 Solución de Problemas

### Problema: "Port 8080 is already in use"

**Solución 1:** Usar otro puerto

```bash
docker run -d -p 8081:3000 --name fresh-market-app andresgarcia09/fresh-market:v2.0
```

Luego accede a: `http://localhost:8081`

**Solución 2:** Encontrar y detener el proceso que usa el puerto

```bash
# Windows (CMD)
netstat -ano | findstr :8080
taskkill /PID <PID_NUMBER> /F

# Windows (PowerShell)
Get-Process -Id (Get-NetTCPConnection -LocalPort 8080).OwningProcess | Stop-Process -Force
```

### Problema: "Error: Cannot find module..."

Esto indica que `yarn install` no se ejecutó correctamente.

**Solución:**

```bash
# Reconstruir la imagen desde cero (sin cache)
docker build --no-cache -t andresgarcia09/fresh-market:v2.0 .
```

### Problema: "Cannot connect to Docker daemon"

**Solución:**

1. Verifica que Docker Desktop esté ejecutándose
2. Reinicia Docker Desktop
3. En la terminal, ejecuta: `docker version`

### Problema: "La página muestra los estilos viejos"

**Solución:**

1. Limpia la caché del navegador: `Ctrl + Shift + R` (Windows)
2. Abre el navegador en modo incógnito
3. Verifica que el contenedor esté usando la nueva imagen:

```bash
docker inspect fresh-market-app | findstr "Image"
```

---

## 📊 Comparación de Versiones

| Característica | v1.0 (Anterior) | v2.0 (Nueva) |
|----------------|-----------------|--------------|
| Aspecto | Lista TODO genérica | Tienda profesional |
| Hero/Banner | ❌ No | ✅ Sí |
| Galería de productos | ❌ No | ✅ Sí (8 productos) |
| Footer | ❌ No | ✅ Sí (completo) |
| Navbar | ❌ No | ✅ Sí (sticky) |
| Paleta de colores | Morado/genérico | Verde/fresco (temático) |
| Responsive | Básico | ✅ Completo |
| Animaciones | Mínimas | ✅ Profesionales |
| SEO | Básico | ✅ Optimizado |
| Créditos | ❌ No | ✅ "AndresGarcia" |

---

## ✅ CHECKLIST FINAL

Antes de dar por terminado, verifica:

- [ ] ✅ Imagen Docker construida correctamente
- [ ] ✅ Contenedor ejecutándose sin errores
- [ ] ✅ Sitio accesible en http://localhost:8080
- [ ] ✅ Todos los elementos visuales presentes
- [ ] ✅ Funcionalidad del carrito operativa
- [ ] ✅ Responsive funcionando en diferentes tamaños
- [ ] ✅ Créditos "AndresGarcia" visibles en el footer
- [ ] ✅ Sin errores en la consola del navegador (F12)

---

## 📞 Soporte

Si tienes problemas o dudas:

1. Revisa el archivo `CHANGELOG_MEJORAS.md` para detalles técnicos
2. Verifica los logs del contenedor: `docker logs fresh-market-app`
3. Asegúrate de que no haya errores en la consola del navegador (F12)

---

## 🎉 ¡Listo!

Tu tienda **Fresh Market** está lista y ejecutándose con un diseño profesional y moderno.

**Desarrollado por:** AndresGcia  
**Versión:** 2.0.0  
**Fecha:** 2024

---

### Comandos Rápidos (Resumen)

```bash
# Construir
docker build -t andresgarcia09/fresh-market:v2.0 .

# Ejecutar
docker run -d -p 8080:3000 --name fresh-market-app andresgarcia09/fresh-market:v2.0

# Ver
http://localhost:8080

# Logs
docker logs fresh-market-app

# Detener
docker stop fresh-market-app

# Limpiar
docker rm fresh-market-app
docker rmi andresgarcia09/fresh-market:v2.0
```
