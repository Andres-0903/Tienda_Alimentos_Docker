# 🚀 GUÍA: Conectar MCP GitHub y Subir al Repositorio

## 📋 Tu Repositorio GitHub

**URL:** https://github.com/Andres-0903/Tienda_Alimentos_Docker

---

## PARTE 1: CONFIGURAR MCP SERVER DE GITHUB

### Paso 1: Instalar UV (Gestor de paquetes Python)

#### En Windows:

**Opción A - PowerShell (Recomendado):**
```powershell
powershell -c "irm https://astral.sh/uv/install.ps1 | iex"
```

**Opción B - Usando pip:**
```bash
pip install uv
```

**Verificar instalación:**
```bash
uv --version
```

### Paso 2: Crear Token de GitHub

1. Ve a: https://github.com/settings/tokens
2. Click en **"Generate new token"** → **"Generate new token (classic)"**
3. Dale un nombre: `Kiro MCP Access`
4. Selecciona los siguientes permisos:
   - ✅ `repo` (todos los sub-permisos)
   - ✅ `workflow`
5. Click en **"Generate token"**
6. **⚠️ COPIA EL TOKEN** (solo se muestra una vez)

### Paso 3: Configurar Token en Windows

**PowerShell (Permanente):**
```powershell
[System.Environment]::SetEnvironmentVariable('GITHUB_TOKEN', 'tu_token_aqui', 'User')
```

**CMD (Permanente):**
```cmd
setx GITHUB_TOKEN "tu_token_aqui"
```

**Temporal (solo sesión actual):**
```powershell
$env:GITHUB_TOKEN="tu_token_aqui"
```

### Paso 4: Reiniciar Kiro

Después de configurar el token:
1. Cierra Kiro completamente
2. Reinicia Kiro
3. El MCP Server de GitHub debería conectarse automáticamente

### Paso 5: Verificar Conexión

En Kiro, puedes verificar que el MCP esté conectado:
- Ve a la vista de MCP Servers en el panel lateral
- Debe aparecer "github" con estado "conectado" (verde)

---

## PARTE 2: SUBIR ARCHIVOS AL REPOSITORIO

### Opción A: Usando Git en la Terminal

```bash
# 1. Ir a la carpeta del proyecto
cd "C:\Users\Andres\Desktop\Curso Docker Udemy\app"

# 2. Inicializar Git (si no está inicializado)
git init

# 3. Configurar tu información (si es primera vez)
git config --global user.name "Andres-0903"
git config --global user.email "tu_email@example.com"

# 4. Agregar el repositorio remoto
git remote add origin https://github.com/Andres-0903/Tienda_Alimentos_Docker.git

# 5. Verificar el remoto
git remote -v

# 6. Crear la rama main (si no existe)
git branch -M main

# 7. Agregar todos los archivos
git add .

# 8. Hacer el primer commit
git commit -m "feat: Initial commit - Fresh Market v2.1.0

- Tienda de alimentos con diseño profesional
- Galería de 8 productos predefinidos
- Carrito de compras funcional
- Diseño responsive
- Dockerizado
- Desarrollado por AndresGarcia"

# 9. Subir al repositorio (primera vez)
git push -u origin main

# Si el repositorio ya tiene contenido, usa:
git pull origin main --rebase
git push -u origin main
```

### Opción B: Si Git pide autenticación

Si te pide usuario y contraseña:

**Usar Token Personal:**
- Usuario: `Andres-0903`
- Contraseña: Tu token de GitHub (el mismo que creaste antes)

**O configurar credential helper:**
```bash
git config --global credential.helper wincred
```

---

## PARTE 3: VERIFICAR QUE TODO ESTÉ SUBIDO

### En GitHub:

1. Ve a: https://github.com/Andres-0903/Tienda_Alimentos_Docker
2. Deberías ver todos estos archivos:

```
✅ src/
   ✅ static/
      ✅ css/styles.css
      ✅ js/app.js
      ✅ index.html
   ✅ persistence/
   ✅ routes/
   ✅ index.js
✅ .kiro/
   ✅ settings/mcp.json
   ✅ steering/git-docker-best-practices.md
✅ .gitignore
✅ .dockerignore
✅ Dockerfile
✅ package.json
✅ README.md
✅ CHANGELOG_MEJORAS.md
✅ INSTRUCCIONES_DEPLOY.md
✅ PROBLEMA_RESUELTO.md
✅ README_QUICK_START.md
✅ RESUMEN_CAMBIOS.md
```

### Archivos que NO deben estar (por .gitignore):

```
❌ node_modules/
❌ etc/todo.db
❌ .DS_Store
❌ *.log
```

---

## 🔧 SOLUCIÓN DE PROBLEMAS

### Problema: "Permission denied (publickey)"

**Solución:** Usar HTTPS en lugar de SSH
```bash
git remote set-url origin https://github.com/Andres-0903/Tienda_Alimentos_Docker.git
```

### Problema: "Repository not found"

**Verificar:**
1. El repositorio existe en GitHub
2. Tu usuario tiene acceso
3. La URL es correcta

### Problema: "Updates were rejected"

Si el repositorio remoto tiene cambios:
```bash
git pull origin main --rebase
git push origin main
```

### Problema: MCP GitHub sigue desconectado

**Checklist:**
1. ✅ `uv` instalado (`uv --version`)
2. ✅ Token configurado (`echo $env:GITHUB_TOKEN` en PowerShell)
3. ✅ Kiro reiniciado completamente
4. ✅ Archivo `mcp.json` existe en `.kiro/settings/`

**Revisar logs:**
- Ve al panel de MCP Servers en Kiro
- Click en el servidor "github"
- Revisa los logs de error

---

## 📝 COMANDOS ÚTILES POST-SETUP

### Ver estado del repositorio:
```bash
git status
```

### Ver historial de commits:
```bash
git log --oneline
```

### Agregar cambios futuros:
```bash
# Ver qué cambió
git status

# Agregar archivos específicos
git add src/static/css/styles.css
git add src/static/index.html

# O agregar todos
git add .

# Commit
git commit -m "feat: descripción del cambio"

# Push
git push origin main
```

### Crear un nuevo branch:
```bash
git checkout -b feature/nueva-funcionalidad
git push -u origin feature/nueva-funcionalidad
```

---

## ✅ CHECKLIST FINAL

Marca cuando completes cada paso:

### Configuración MCP:
- [ ] UV instalado
- [ ] Token de GitHub creado
- [ ] Token configurado en variable de entorno
- [ ] Kiro reiniciado
- [ ] MCP "github" conectado (verde)

### Subida a GitHub:
- [ ] Git inicializado
- [ ] Remoto configurado
- [ ] Archivos agregados con `git add .`
- [ ] Commit realizado
- [ ] Push exitoso a GitHub
- [ ] Archivos visibles en https://github.com/Andres-0903/Tienda_Alimentos_Docker

### Verificación:
- [ ] README.md se ve bien en GitHub
- [ ] No hay archivos sensibles (node_modules, .db)
- [ ] .gitignore funciona correctamente
- [ ] Puedes clonar el repo en otra carpeta de prueba

---

## 🎉 ¡TODO LISTO!

Una vez completado:

1. Tu proyecto estará en GitHub
2. Podrás usar MCP para interactuar con el repositorio
3. Otros podrán clonar y usar tu proyecto
4. Tendrás backup de todo tu código

---

## 📞 SIGUIENTE PASO

Avísame cuando:
1. Hayas configurado el token de GitHub
2. Hayas subido los archivos al repo

Y te ayudo con cualquier error que aparezca o con los siguientes pasos.

---

**Desarrollado por:** AndresGarcia  
**Repositorio:** https://github.com/Andres-0903/Tienda_Alimentos_Docker
