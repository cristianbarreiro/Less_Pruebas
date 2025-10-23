# 🎨 LESS - Leaner Style Sheets

![LESS Logo](https://lesscss.org/public/img/less_logo.png)

## 📖 Índice

- [¿Qué es LESS?](#qué-es-less)
- [Instalación en Fedora Workstation](#instalación-en-fedora-workstation)
- [Uso Básico](#uso-básico)
- [Funcionalidades Principales](#funcionalidades-principales)
- [Ventajas y Mejoras](#ventajas-y-mejoras)
- [Comandos Útiles](#comandos-útiles)
- [Ejemplos Prácticos](#ejemplos-prácticos)
- [Estructura del Proyecto](#estructura-del-proyecto)

## ¿Qué es LESS?

LESS (Leaner Style Sheets) es un **preprocesador de CSS** que extiende las capacidades del CSS tradicional con características como variables, mixins, funciones y operaciones matemáticas. LESS se compila a CSS estándar, lo que permite escribir código más mantenible, reutilizable y organizado.

### 🚀 Características Principales

- **Variables**: Almacena valores reutilizables
- **Mixins**: Reutilización de conjuntos de propiedades CSS
- **Funciones**: Manipulación de colores y valores
- **Operaciones matemáticas**: Cálculos dinámicos
- **Anidación**: Estructura jerárquica similar a HTML
- **Importaciones**: Modularización del código
- **Compilación automática**: Conversión a CSS estándar

## 📦 Instalación en Fedora Workstation

### Paso 1: Instalación de Node.js y npm

```bash
# Actualizar el sistema
sudo dnf update -y

# Instalar Node.js y npm desde los repositorios oficiales
sudo dnf install nodejs npm -y

# Verificar la instalación
node --version
npm --version
```

### Paso 2: Instalación de LESS

```bash
# Instalación global de LESS
sudo npm install -g less

# Verificar la instalación
lessc --version
```

### Instalación Alternativa (usando Node Version Manager - NVM)

```bash
# Instalar NVM
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash

# Recargar el shell
source ~/.bashrc

# Instalar la última versión LTS de Node.js
nvm install --lts
nvm use --lts

# Instalar LESS
npm install -g less
```

## 🔧 Uso Básico

### Comando de Compilación

```bash
# Sintaxis básica
lessc archivo-fuente.less archivo-destino.css

# Ejemplo práctico (como en tu proyecto)
root@fedora:/home/one/Descargas/Less_Pruebas/parte1# lessc styles.less styles.css

# Compilación con minificación
lessc styles.less styles.min.css --compress

# Compilación con source maps para debugging
lessc styles.less styles.css --source-map
```

### Opciones de Compilación Útiles

```bash
# Compilación automática (watch mode)
lessc styles.less styles.css --watch

# Compilación con información detallada
lessc styles.less styles.css --verbose

# Ver ayuda de comandos
lessc --help
```

## 🛠️ Funcionalidades Principales

### 1. Variables

Las variables permiten almacenar valores que se pueden reutilizar en todo el código.

```less
// Definición de variables
@color-primario: #3498db;
@color-secundario: #2ecc71;
@fuente-principal: 'Helvetica Neue', sans-serif;
@tamaño-base: 16px;

// Uso de variables
body {
    font-family: @fuente-principal;
    font-size: @tamaño-base;
    color: @color-primario;
}
```

### 2. Mixins

Los mixins permiten definir grupos de propiedades CSS que se pueden reutilizar.

```less
// Definición de mixin
.border-radius(@radius: 5px) {
    border-radius: @radius;
    -webkit-border-radius: @radius;
    -moz-border-radius: @radius;
}

// Uso del mixin
.button {
    .border-radius(10px);
    background: @color-primario;
}
```

### 3. Anidación

Permite escribir selectores de forma jerárquica, similar a la estructura HTML.

```less
.navegacion {
    background: @color-primario;
    
    ul {
        list-style: none;
        margin: 0;
        
        li {
            display: inline-block;
            
            a {
                text-decoration: none;
                color: white;
                
                &:hover {
                    color: @color-secundario;
                }
            }
        }
    }
}
```

### 4. Funciones y Operaciones

LESS incluye funciones matemáticas y de manipulación de colores.

```less
@color-base: #3498db;

.header {
    background: @color-base;
    border: 1px solid darken(@color-base, 20%);
    color: lighten(@color-base, 40%);
    margin: (10px * 2);
    width: (100% / 3);
}
```

### 5. Importación de Archivos

Permite dividir el código en múltiples archivos para mejor organización.

```less
// variables.less
@import "variables.less";
@import "mixins.less";
@import "components/buttons.less";

.main-content {
    // Tu código aquí
}
```

## 🎯 Ventajas y Mejoras

### ✅ Ventajas de LESS sobre CSS tradicional

1. **Mantenibilidad**: Las variables facilitan cambios globales
2. **Reutilización**: Los mixins evitan código repetitivo
3. **Organización**: La anidación mejora la legibilidad
4. **Funcionalidad**: Operaciones matemáticas y funciones incorporadas
5. **Modularidad**: Sistema de importación para dividir archivos
6. **Compatibilidad**: Se compila a CSS estándar
7. **Desarrollo más rápido**: Menos código, más funcionalidad

### 🔄 Comparación: LESS vs CSS

| Característica | CSS | LESS |
|---------------|-----|------|
| Variables | ❌ (solo CSS custom properties) | ✅ |
| Mixins | ❌ | ✅ |
| Anidación | ❌ | ✅ |
| Funciones | ❌ | ✅ |
| Operaciones matemáticas | ❌ | ✅ |
| Compilación | No necesaria | Requerida |

## 📋 Comandos Útiles

### Comandos de NPM para LESS

```bash
# Instalación local en un proyecto
npm install less --save-dev

# Actualizar LESS
sudo npm update -g less

# Desinstalar LESS
sudo npm uninstall -g less

# Ver información del paquete
npm info less
```

### Scripts de Package.json

Puedes automatizar la compilación agregando scripts en `package.json`:

```json
{
  "scripts": {
    "build-css": "lessc styles.less styles.css",
    "watch-css": "lessc styles.less styles.css --watch",
    "build-min": "lessc styles.less styles.min.css --compress"
  }
}
```

### Automatización con Makefile

```makefile
# Crear un Makefile para automatizar tareas
css:
	lessc styles.less styles.css

css-min:
	lessc styles.less styles.min.css --compress

watch:
	lessc styles.less styles.css --watch

.PHONY: css css-min watch
```

## 💡 Ejemplos Prácticos

### Ejemplo Completo: Sistema de Colores

```less
// variables.less
@color-primario: #3498db;
@color-secundario: #2ecc71;
@color-peligro: #e74c3c;
@color-advertencia: #f39c12;

// mixins.less
.button-style(@bg-color) {
    background: @bg-color;
    color: white;
    border: none;
    padding: 10px 20px;
    border-radius: 5px;
    cursor: pointer;
    
    &:hover {
        background: darken(@bg-color, 10%);
    }
}

// main.less
@import "variables.less";
@import "mixins.less";

.btn-primary {
    .button-style(@color-primario);
}

.btn-success {
    .button-style(@color-secundario);
}

.btn-danger {
    .button-style(@color-peligro);
}
```

### Ejemplo: Grid System Responsivo

```less
@container-width: 1200px;
@gutter: 30px;

.container {
    max-width: @container-width;
    margin: 0 auto;
    padding: 0 (@gutter / 2);
}

.row {
    margin: 0 (-@gutter / 2);
    
    &:after {
        content: "";
        display: table;
        clear: both;
    }
}

.col(@columns) {
    width: (100% / 12 * @columns);
    float: left;
    padding: 0 (@gutter / 2);
}

// Generar clases de columnas
.col-1 { .col(1); }
.col-2 { .col(2); }
.col-3 { .col(3); }
// ... hasta col-12
```

## 📁 Estructura del Proyecto

```
Less_Pruebas/parte1/
├── README.md              # Este archivo
├── index.html            # Archivo HTML principal
├── styles.less           # Archivo fuente LESS
├── styles.css            # Archivo CSS compilado
├── package.json          # Configuración de npm (opcional)
└── src/                  # Carpeta para archivos LESS modulares
    ├── variables.less
    ├── mixins.less
    ├── components/
    │   ├── buttons.less
    │   └── navigation.less
    └── layouts/
        ├── grid.less
        └── responsive.less
```

## 🐛 Solución de Problemas Comunes

### Error: "lessc: command not found"

```bash
# Verificar que npm esté instalado
npm --version

# Reinstalar LESS globalmente
sudo npm install -g less

# Verificar el PATH
echo $PATH
```

### Error de permisos en Fedora

```bash
# Si hay problemas de permisos, usar sudo
sudo npm install -g less

# O configurar npm para usar un directorio local
npm config set prefix '~/.npm-global'
echo 'export PATH=~/.npm-global/bin:$PATH' >> ~/.bashrc
source ~/.bashrc
```

### Problemas de compilación

```bash
# Verificar sintaxis del archivo LESS
lessc styles.less --lint

# Compilar con información de debug
lessc styles.less styles.css --verbose
```

## 🔗 Recursos Adicionales

- **Sitio oficial**: https://lesscss.org/
- **Documentación**: https://lesscss.org/features/
- **GitHub**: https://github.com/less/less.js
- **Playground online**: https://lesscss.org/less-preview/

## 📝 Notas del Proyecto Actual

En este proyecto tienes:

- **Variables definidas**: `@base-color`, `@color-principal`, `@color-secundario`, `@fuente`
- **Función de color**: `darken(@color-principal, 10%)`
- **Estructura básica**: HTML con estilos LESS compilados a CSS

### Comando utilizado en tu proyecto:
```bash
root@fedora:/home/one/Descargas/Less_Pruebas/parte1# lessc styles.less styles.css
```

---

*README creado para el proyecto de aprendizaje de LESS en Fedora Workstation*