# ⚡ QUICK START - Fresh Market

## 🚀 Inicio Rápido en 3 Pasos

### 1️⃣ Construir la imagen:
```bash
cd "C:\Users\Andres\Desktop\Curso Docker Udemy\app"
docker build -t andresgarcia09/fresh-market:v2.1 .
```

### 2️⃣ Ejecutar el contenedor:
```bash
docker run -d -p 8080:3000 --name fresh-market-app andresgarcia09/fresh-market:v2.1
```

### 3️⃣ Abrir en el navegador:
```
http://localhost:8080
```

---

## 🐛 BUG FIX v2.1

✅ **PROBLEMA RESUELTO:** El botón "Añadir Alimento" ahora funciona correctamente.

**¿Qué se corrigió?**
- Botón `type="Enviar"` → `type="submit"` (correcto)
- Ahora los productos se agregan al carrito sin problemas

Ver detalles en: `PROBLEMA_RESUELTO.md`

---

## ✨ Qué hay de nuevo

### Visual:
- 🏪 **Navbar** profesional con logo y navegación
- 🌿 **Hero banner** verde con título atractivo
- 🛒 **Galería de 8 productos** con precios y botones
- 🛍️ **Carrito funcional** para administrar compras
- 📱 **Footer completo** con créditos "Desarrollado por AndresGarcia"
- 🎨 **Diseño responsive** para móvil, tablet y desktop
- ✨ **Animaciones suaves** y profesionales

### Técnico:
- ✅ HTML5 semántico
- ✅ CSS con variables modernas
- ✅ Backend sin modificar
- ✅ React funcionando igual
- ✅ Docker compatible
- ✅ Solo ~8 KB añadidos

---

## 🎨 Paleta de Colores

```
Verde:  #10B981  (Principal)
Naranja: #F59E0B  (Acentos)
Fondo:   #F9FAFB  (Claro)
Texto:   #1F2937  (Oscuro)
```

---

## 📦 Productos Disponibles

1. 🍎 Manzanas Rojas - $2.99/kg
2. 🥕 Zanahorias Orgánicas - $1.99/kg
3. 🥬 Lechuga Fresca - $1.49/ud
4. 🍊 Naranjas Valencianas - $3.49/kg
5. 🥦 Brócoli Verde - $2.29/kg
6. 🍓 Fresas Premium - $4.99/kg
7. 🍌 Plátanos - $1.79/kg
8. 🥑 Aguacates Hass - $5.99/kg

---

## 🛠️ Comandos Útiles

### Ver logs:
```bash
docker logs fresh-market-app
```

### Detener:
```bash
docker stop fresh-market-app
```

### Reiniciar:
```bash
docker restart fresh-market-app
```

### Limpiar:
```bash
docker stop fresh-market-app
docker rm fresh-market-app
docker rmi andresgarcia09/fresh-market:v2.1
```

---

## 📚 Documentación Completa

- `RESUMEN_CAMBIOS.md` - Resumen visual de todos los cambios
- `CHANGELOG_MEJORAS.md` - Detalles técnicos completos
- `INSTRUCCIONES_DEPLOY.md` - Guía de despliegue detallada

---

## ✅ Checklist Rápido

- [ ] Imagen construida
- [ ] Contenedor corriendo
- [ ] Sitio accesible en http://localhost:8080
- [ ] Hero banner visible
- [ ] Galería de 8 productos funcional
- [ ] Botones "Agregar" funcionando
- [ ] Carrito operativo
- [ ] Footer con créditos "AndresGarcia"
- [ ] Responsive OK

---

## 🎉 ¡Listo!

Tu tienda **Fresh Market** está funcionando con diseño profesional.

**Desarrollado por:** AndresGarcia  
**Versión:** 2.1 (Bug Fix - Botón agregar corregido)  
**Puerto:** 8080  
**URL:** http://localhost:8080

---

## 🆘 Problema Común

### "Puerto 8080 en uso"
```bash
# Usar otro puerto
docker run -d -p 8081:3000 --name fresh-market-app andresgarcia09/fresh-market:v2.1

# Acceder en: http://localhost:8081
```

---

**¿Necesitas ayuda?** Consulta `INSTRUCCIONES_DEPLOY.md` para solución de problemas.

**¿Botón no funciona?** Consulta `PROBLEMA_RESUELTO.md` para el fix aplicado.
