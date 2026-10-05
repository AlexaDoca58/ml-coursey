# AGENTS.md

Instrucciones para agentes de IA (Codex, Claude Code, Cursor, Copilot, etc.) que trabajen en este repositorio.

## Contexto

Este es el repositorio de un **curso introductorio de Machine Learning**. Quien te pide ayuda es, muy probablemente, un **alumno que está aprendiendo**. Tu objetivo es ayudarle a entender, no solo a terminar la tarea.

- Idioma del curso: **español**. Responde y escribe comentarios y Markdown en español. El código (nombres de variables y funciones) puede ir en inglés.
- Explica el *porqué* de lo que haces, con un nivel apropiado para principiantes.
- En los **ejercicios** (`notebooks/exercises/`, `projects/`), da pistas y explica el concepto antes de escribir la solución completa, salvo que el alumno pida explícitamente la solución.
- Prefiere código simple y legible a código ingenioso o muy optimizado.

## Entorno

- Python **3.12**, gestionado con **[uv](https://docs.astral.sh/uv/)**.
- Instalar o actualizar el entorno: `uv sync`
- Ejecutar scripts: `uv run python <script>.py`
- Abrir Jupyter: `uv run --with jupyter jupyter lab`
- Añadir una dependencia: `uv add <paquete>`. **No** uses `pip install` ni edites `uv.lock` a mano.
- Guía completa de instalación: [docs/installation.md](docs/installation.md)

## Estructura

```
data/                       # Datasets (no se versionan)
docs/                       # Guías: instalación, uso del repo, SSH de GitHub
notebooks/
  lectures/chapter_XX/      # Notebooks de clase
  exercises/chapter_XX/     # Ejercicios para el alumno
projects/chapter_XX/        # Proyectos prácticos
scripts/                    # Utilidades (p. ej. download_data.py)
workspace/                  # Carpeta de trabajo del alumno
```

- El alumno trabaja en un **fork** que se sincroniza con el repo del profesor. **Solo modifica archivos dentro de `workspace/`.** Si hay que resolver un notebook del curso, cópialo primero a `workspace/` y edita la copia. Editar los archivos del curso provoca conflictos al sincronizar.

- Nombres de notebooks: `NN_tema.ipynb` (por ejemplo, `00_intro_to_jupyter.ipynb`).
- Los datos se descargan con `uv run python scripts/download_data.py` y se guardan en `data/`.

## Reglas

- **No subas datos ni modelos a Git.** `data/`, `*.csv`, `*.pkl`, `*.pt`, etc. están en `.gitignore`; no los fuerces con `git add -f`.
- **No escribas secretos** (API keys, contraseñas, tokens) en código ni en notebooks. Usa variables de entorno o un archivo `.env`, que está ignorado por Git.
- **Notebooks reproducibles:** deben funcionar con *Restart & Run All*, de arriba abajo, con los imports al principio.
- **Limpia las salidas** de los notebooks antes de hacer commit.
- Usa rutas relativas a la raíz del repo, no rutas absolutas de tu computadora.
- Fija semillas aleatorias (`random_state=42`, `np.random.seed(42)`) para que los resultados sean reproducibles.
- No hagas `git commit` ni `git push` sin que el alumno lo pida.
