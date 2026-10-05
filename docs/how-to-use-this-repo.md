# Cómo usar este repositorio

Esta guía es para ti si **nunca has usado GitHub**. Al terminar tendrás tu propia copia del curso, podrás guardar tus ejercicios en internet y recibirás las actualizaciones que el profesor publique durante el curso.

---

## Contenido

0. [Conceptos básicos](#0-conceptos-básicos-2-minutos)
1. [Crear tu copia del curso (fork)](#1-crear-tu-copia-del-curso-fork)
2. [Descargar tu copia a tu computadora (clone)](#2-descargar-tu-copia-a-tu-computadora-clone)
3. [Trabajar en la carpeta `workspace/`](#3-trabajar-en-la-carpeta-workspace)
4. [Guardar tu trabajo en GitHub](#4-guardar-tu-trabajo-en-github)
5. [Recibir las actualizaciones del curso](#5-recibir-las-actualizaciones-del-curso)
6. [Resumen: tu rutina en cada clase](#6-resumen-tu-rutina-en-cada-clase)
7. [Problemas comunes](#7-problemas-comunes)

---

## 0. Conceptos básicos (2 minutos)

| Palabra | Qué significa |
|---|---|
| **Git** | Programa que guarda el historial de cambios de tus archivos, como un "control de versiones". |
| **GitHub** | Página web donde se guardan proyectos de Git en internet. |
| **Repositorio (repo)** | Una carpeta de proyecto con su historial. Este curso es un repo. |
| **Fork** | Tu **copia personal** del repo del curso, dentro de tu cuenta de GitHub. |
| **Clone** | Descargar un repo de GitHub a tu computadora. |
| **Commit** | Una "foto" de tus cambios con un mensaje que describe qué hiciste. |
| **Push** | Subir tus commits de tu computadora a GitHub. |
| **Pull** | Bajar a tu computadora los cambios que hay en GitHub. |

**La idea general:**

```
Repo del profesor  ──(fork)──▶  Tu repo en GitHub  ──(clone)──▶  Tu computadora
       │                              ▲    │                          │
       └──── actualizaciones ─────────┘    └──────── pull ───────────▶│
              (Sync fork)                  ◀──────── push ────────────┘
```

- El profesor actualiza **su** repo.
- Tú traes esas actualizaciones a **tu** fork con un botón (**Sync fork**).
- Tú guardas **tus** ejercicios en **tu** fork con `push`.
- Tus cambios **nunca** llegan al repo del profesor, así que no puedes romper nada.

---

## 1. Crear tu copia del curso (fork)

1. Crea una cuenta en <https://github.com> si no tienes una.
2. Entra al repo del curso: <https://github.com/riosinda/ml-course>
3. Arriba a la derecha, haz clic en **Fork**.
4. Deja todo como está y haz clic en **Create fork**.

Ahora tienes tu copia en `https://github.com/TU-USUARIO/ml-course`. 🎉

> Tu fork es **público**: cualquiera puede ver lo que subas.

---

## 2. Descargar tu copia a tu computadora (clone)

**Antes de este paso:**

- Instala Git, uv y Python: [docs/installation.md](installation.md), pasos 1 a 3.
- Configura SSH para poder subir cambios: [docs/github-ssh.md](github-ssh.md).

Abre una terminal (en Windows, PowerShell) y ve a la carpeta donde quieres guardar el curso. Por ejemplo, Documentos:

```bash
cd ~/Documents
```

Clona **tu fork**, no el del profesor. Cambia `TU-USUARIO` por tu usuario de GitHub:

```bash
git clone git@github.com:TU-USUARIO/ml-course.git
cd ml-course
uv sync
```

> 💡 Puedes copiar la dirección exacta desde tu fork en GitHub: botón verde **Code → SSH**.

Abre la carpeta `ml-course` en VS Code: **File → Open Folder…**

---

## 3. Trabajar en la carpeta `workspace/`

Esta es **la regla más importante del curso**:

> ⚠️ **No modifiques los archivos del curso.** Trabaja siempre dentro de `workspace/`.

¿Por qué? El profesor actualizará los notebooks durante el curso. Si tú también los modificas, al recibir las actualizaciones Git no sabrá qué versión conservar y tendrás un **conflicto**. Si trabajas solo en `workspace/`, eso nunca pasa.

```
ml-course/
├── notebooks/     ← del profesor: solo abrir y ejecutar
├── projects/      ← del profesor: solo abrir y ejecutar
└── workspace/     ← TUYO: aquí resuelves los ejercicios
```

### Cómo empezar un ejercicio

Copia el notebook a `workspace/` y trabaja sobre la copia.

**Opción A: en VS Code.** Clic derecho sobre el notebook → **Copy**. Luego clic derecho sobre `workspace/` → **Paste**.

**Opción B: en la terminal** (funciona igual en macOS, Linux y PowerShell):

```bash
cp notebooks/exercises/chapter_03/01_ejercicios.ipynb workspace/
```

Puedes organizar `workspace/` como quieras. Por ejemplo, con una carpeta por capítulo: `workspace/chapter_03/`.

> Abrir y ejecutar los notebooks de clase sin guardar cambios está bien. Si VS Code te pregunta si quieres guardar al cerrarlos, elige **Don't Save**.

---

## 4. Guardar tu trabajo en GitHub

Cuando termines algo que quieras guardar, sube tus cambios con tres comandos:

```bash
git add workspace/
git commit -m "Resuelvo ejercicios del capítulo 3"
git push
```

| Comando | Qué hace |
|---|---|
| `git add workspace/` | Selecciona los cambios de tu carpeta para la "foto" |
| `git commit -m "..."` | Toma la foto, con un mensaje que describe qué hiciste |
| `git push` | Sube la foto a tu fork en GitHub |

Para ver qué archivos cambiaste antes de hacer commit:

```bash
git status
```

### Alternativa sin terminal: VS Code

1. Abre el panel **Source Control** (icono de ramas a la izquierda, o `Ctrl + Shift + G`).
2. Junto a cada archivo de `workspace/`, haz clic en **+** (equivale a `git add`).
3. Escribe un mensaje arriba y haz clic en **Commit**.
4. Haz clic en **Sync Changes** (equivale a `git push`).

---

## 5. Recibir las actualizaciones del curso

Cuando el profesor publique contenido nuevo, haz dos pasos.

**Paso 1: actualiza tu fork en GitHub**

1. Entra a tu fork: `https://github.com/TU-USUARIO/ml-course`
2. Haz clic en **Sync fork** y luego en **Update branch**.

**Paso 2: baja los cambios a tu computadora**

```bash
git pull
uv sync
```

`uv sync` instala las librerías nuevas, si el profesor añadió alguna.

> ⚠️ Si GitHub te muestra un botón **Discard commits**, **no lo pulses**: borraría tu trabajo. Mira [Problemas comunes](#7-problemas-comunes).

---

## 6. Resumen: tu rutina en cada clase

**Al empezar:**

1. GitHub → tu fork → **Sync fork** → **Update branch**.
2. En la terminal: `git pull` y luego `uv sync`.

**Durante la clase:**

3. Copia a `workspace/` los notebooks que vayas a resolver y trabaja ahí.

**Al terminar:**

4. En la terminal: `git add workspace/`, luego `git commit -m "mensaje"`, luego `git push`.

---

## 7. Problemas comunes

### `git pull` dice: *"Your local changes would be overwritten"*

Modificaste un archivo del curso. Si quieres conservar tus cambios, primero copia ese archivo a `workspace/`. Después devuelve el original a su estado:

```bash
git restore notebooks/ruta/del/archivo.ipynb
git pull
```

### `git push` dice: *"rejected"* o *"fetch first"*

Tu fork en GitHub tiene cambios que tu computadora no tiene, normalmente porque hiciste **Sync fork**. Baja esos cambios primero:

```bash
git pull
git push
```

### **Sync fork** muestra *"This branch has conflicts"* o un botón **Discard commits**

Hiciste commit de cambios en archivos del curso, fuera de `workspace/`. **No pulses Discard commits**: pide ayuda al profesor.

### `git push` dice: *"Permission denied (publickey)"*

SSH no está configurado. Sigue [docs/github-ssh.md](github-ssh.md).

### ¿Puedo proponer cambios al repo del profesor (Pull Request)?

Este repo **no acepta Pull Requests**. Si encuentras un error en el material, avísale al profesor directamente.
