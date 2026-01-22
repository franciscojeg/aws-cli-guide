# 🚀 Instrucciones para Subir a GitHub

## Paso 1: Crear el Repositorio en GitHub

1. Ve a [github.com](https://github.com) e inicia sesión
2. Haz clic en el botón **"+"** (esquina superior derecha) → **"New repository"**
3. Configura el repositorio:
   - **Repository name:** `aws-cli-guide`
   - **Description:** `📚 Guía completa de comandos AWS CLI para debugging, monitoreo y administración`
   - **Visibility:** Public (para que sea accesible)
   - ⚠️ **NO** marques "Add a README file" (ya tenemos uno)
   - ⚠️ **NO** agregues .gitignore ni licencia (ya los tenemos)
4. Haz clic en **"Create repository"**

## Paso 2: Configurar Git Localmente

### Si NO tienes Git instalado:

```bash
# macOS
brew install git

# Linux (Ubuntu/Debian)
sudo apt-get install git

# Windows
# Descarga desde: https://git-scm.com/download/win
```

### Configurar tu identidad (solo la primera vez):

```bash
git config --global user.name "Francisco Javier Escobar García"
git config --global user.email "tu-email@ejemplo.com"
```

## Paso 3: Preparar los Archivos

Descarga el archivo ZIP del repositorio que te proporcioné y descomprímelo, o crea la estructura manualmente:

```
aws-cli-guide/
├── README.md
├── README_ES.md
├── LICENSE
├── CONTRIBUTING.md
├── .gitignore
└── docs/
    ├── Guia_AWS_CLI_Commands.docx
    └── AWS_CLI_Guide.md
```

## Paso 4: Inicializar y Subir el Repositorio

Abre la terminal, navega a la carpeta del proyecto y ejecuta estos comandos:

```bash
# Navegar a la carpeta del proyecto
cd ruta/a/aws-cli-guide

# Inicializar el repositorio Git
git init

# Agregar todos los archivos
git add .

# Crear el primer commit
git commit -m "🎉 Initial commit: AWS CLI Guide"

# Renombrar la rama principal a 'main'
git branch -M main

# Conectar con tu repositorio de GitHub (reemplaza TU-USUARIO)
git remote add origin https://github.com/TU-USUARIO/aws-cli-guide.git

# Subir los archivos a GitHub
git push -u origin main
```

## Paso 5: Personalizar el README

Después de subir, edita los READMEs para actualizar:

1. **Links de badges** - Reemplaza `your-username` con tu usuario real
2. **Links de autor** - Agrega tu LinkedIn y perfil de GitHub
3. **Links de Issues** - Se actualizarán automáticamente

### Editar directamente en GitHub:
1. Ve a tu repositorio
2. Haz clic en `README.md`
3. Haz clic en el ícono de lápiz (✏️ Edit)
4. Reemplaza `your-username` con tu usuario de GitHub
5. Haz clic en **"Commit changes"**

## Paso 6: Configuraciones Adicionales (Opcional)

### Agregar Topics/Tags al Repositorio:
1. En la página principal del repo, haz clic en ⚙️ junto a "About"
2. Agrega topics como:
   - `aws`
   - `aws-cli`
   - `cloud`
   - `devops`
   - `cheatsheet`
   - `spanish`

### Habilitar GitHub Pages (para visualizar el Markdown online):
1. Ve a **Settings** → **Pages**
2. Source: **Deploy from a branch**
3. Branch: **main** / **/ (root)**
4. Haz clic en **Save**

### Agregar una Descripción y Website:
1. En la página principal del repo, haz clic en ⚙️ junto a "About"
2. Agrega una descripción corta
3. Agrega tu website o LinkedIn si quieres

---

## 📝 Comandos Git Útiles para el Futuro

```bash
# Ver estado de cambios
git status

# Agregar cambios específicos
git add nombre-archivo

# Agregar todos los cambios
git add .

# Crear commit con mensaje
git commit -m "Descripción del cambio"

# Subir cambios a GitHub
git push

# Descargar cambios de GitHub
git pull

# Ver historial de commits
git log --oneline
```

---

## ✅ Checklist Final

- [ ] Repositorio creado en GitHub
- [ ] Git configurado con tu nombre y email
- [ ] Archivos subidos exitosamente
- [ ] README actualizado con tu usuario real
- [ ] Topics agregados al repositorio
- [ ] ¡Compartir en LinkedIn! 🎉

---

## 🔗 Links Útiles

- [Documentación de Git](https://git-scm.com/doc)
- [GitHub Docs](https://docs.github.com)
- [GitHub Desktop](https://desktop.github.com) (alternativa visual a la terminal)

---

¡Éxito con tu repositorio! 🚀
