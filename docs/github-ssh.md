# Conectar GitHub por SSH

Configura una clave SSH una sola vez y podrás hacer `git clone`, `git pull` y `git push` sin escribir usuario ni token.

Los pasos son para **macOS**, **Linux** y **Windows (PowerShell)**. Cuando un comando es igual en los tres sistemas, aparece una sola vez.

---

## 1. Generar la clave

Usa el email de tu cuenta de GitHub:

```bash
ssh-keygen -t ed25519 -C "tu-email@ejemplo.com"
```

Pulsa `Enter` para aceptar la ruta por defecto. La *passphrase* es opcional: puedes dejarla vacía o poner una contraseña.

Se crean dos archivos en la carpeta `.ssh` de tu usuario:

- `id_ed25519` → clave **privada**. ❌ No la compartas nunca.
- `id_ed25519.pub` → clave **pública**. ✅ Es la que se pega en GitHub.

> **Windows:** si `ssh-keygen` no se reconoce, instala [Git para Windows](https://git-scm.com/download/win) y vuelve a abrir PowerShell.

## 2. Agregar la clave al agente SSH

**macOS / Linux**

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

**Windows (PowerShell)**

Activa el agente una sola vez, desde PowerShell **como administrador**:

```powershell
Get-Service -Name ssh-agent | Set-Service -StartupType Automatic
Start-Service ssh-agent
```

Después, en una PowerShell normal:

```powershell
ssh-add $env:USERPROFILE\.ssh\id_ed25519
git config --global core.sshCommand "C:/Windows/System32/OpenSSH/ssh.exe"
```

La última línea hace que Git use el SSH de Windows, que es el que tiene tu clave cargada.

## 3. Copiar la clave pública

| Sistema | Comando |
|---|---|
| macOS | `pbcopy < ~/.ssh/id_ed25519.pub` |
| Linux | `cat ~/.ssh/id_ed25519.pub` y copia la salida |
| Windows (PowerShell) | `Get-Content $env:USERPROFILE\.ssh\id_ed25519.pub \| Set-Clipboard` |

La clave es una sola línea que empieza con `ssh-ed25519 AAAA...`.

## 4. Agregar la clave en GitHub

1. Ve a **GitHub → Settings → SSH and GPG keys** (<https://github.com/settings/keys>).
2. Haz clic en **New SSH key**.
3. **Title:** un nombre para tu computadora, por ejemplo `laptop-personal`.
4. **Key:** pega la clave.
5. Haz clic en **Add SSH key**.

## 5. Verificar la conexión

```bash
ssh -T git@github.com
```

La primera vez te preguntará `Are you sure you want to continue connecting?`. Escribe `yes`.

Si todo salió bien, verás:

```
Hi tu-usuario! You've successfully authenticated, but GitHub does not provide shell access.
```

## 6. Configurar tu nombre y email en Git

Una sola vez por computadora:

```bash
git config --global user.name "Tu Nombre"
git config --global user.email "tu-email@ejemplo.com"
git config --global pull.rebase true
```

La última línea evita un error de `git pull` cuando tu computadora y GitHub tienen cambios distintos.

## 7. Clonar con SSH

En **tu fork** en GitHub, usa el botón **Code → SSH**:

```bash
git clone git@github.com:TU-USUARIO/ml-course.git
```

¿Ya lo habías clonado con HTTPS? Cambia la URL:

```bash
git remote set-url origin git@github.com:TU-USUARIO/ml-course.git
```

---

## Problemas comunes

**`Permission denied (publickey)`**
Comprueba que la clave está cargada con `ssh-add -l`. Si no aparece, repite el paso 2. Revisa también que en GitHub pegaste el archivo **`.pub`**.

**Windows: `Error connecting to agent`**
El servicio `ssh-agent` no está activo. Repite el paso 2 en PowerShell como administrador.

---

📚 Más detalles: [documentación oficial de GitHub](https://docs.github.com/es/authentication/connecting-to-github-with-ssh)
