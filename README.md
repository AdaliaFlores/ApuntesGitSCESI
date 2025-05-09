# ApuntesGitSCESI

# Introducción al Control de Versiones
---

## ¿Qué es un Control de Versiones?

Un sistema de control de versiones es una herramienta que registra cada cambio que se realiza en el código fuente de un proyecto. Permite:

- Mejor rendimiento, ya que solo guarda lo necesario.
- Seguridad: conserva todas las acciones y quién las realizó.
- Recuperación de cualquier versión anterior.
- Trabajo colaborativo en paralelo sin conflictos.

---

## Breve Historia

| Año  | Evento                                  |
|------|------------------------------------------|
| 1990 | Nace **CVS**, primer sistema de control de versiones. |
| 2005 | Creación de **Git** por la comunidad de desarrollo de Linux. |
| 2008 | Nace **GitHub** para alojar proyectos públicos. |
| 2018 | Microsoft compra GitHub. |
| 2024 | Git domina el mercado. |

> ⚡ Git puede conectarse también con BitBucket o GitLab. Facebook tiene su propia herramienta de control de versiones.

---

## ¿Qué es Git?

Es una herramienta de control de versiones distribuido. Puede tener uno o varios repositorios remotos para estar sincronizado con equipos de trabajo.

---

## ¿Qué es un Repositorio?

Un repositorio es una carpeta que almacena todos los archivos del proyecto y lleva un historial de cambios realizados en ellos.

---

## Crear un Repositorio Git

Puedes crear un nuevo repositorio con:

```bash
git init nombredelproyecto
cd nombredelproyecto
```


# Estados y Commits en Git

---
## Los 3 Estados de Git

Git utiliza un flujo basado en tres estados principales para el control de versiones:

1. **MODIFIED**  
   El archivo ha sido creado, modificado o eliminado, pero **aún no ha sido marcado para el commit** (no está en staging).  
    Se detectan con:  
   ```bash
   git status
   ```

2. **STAGED**  
   El archivo ha sido **marcado como preparado para ser confirmado** en el repositorio local.  
    Para mover un archivo a este estado:  
   ```bash
   git add nombreArchivo
   ```
    Para agregar todos los archivos modificados:  
   ```bash
   git add .
   ```

3. **COMMITTED**  
   El archivo ha sido **registrado en el repositorio local**, ya forma parte de un commit.

---

## ¿Qué es un Commit?

Un **commit** es una "fotografía" del estado actual de los archivos, que se guarda en el historial de Git. Incluye:

- Cambios realizados
- Autor
- Fecha
- Mensaje descriptivo

Es una **pieza fundamental** del control de versiones en Git.

---

## Cómo Hacer un Commit

1. Tener cambios en estado `STAGED`.
2. Ejecuta el comando:
   ```bash
   git commit -m "Mensaje descriptivo del commit"
   ```
   💡 *Es buena práctica usar mensajes claros y concisos.*

---

## 🔁 Restaurar Cambios

Si agregaste un archivo por error al `staging`, se puede deshacer con:
```bash
git restore --staged nombreArchivo
```

---

## Situación: Solo quiero hacer commit de uno de varios archivos modificados

Puedes hacer `git add` **solo al archivo específico** que deseas confirmar:

```bash
git add archivoDeseado
git commit -m "Commit específico"
```

---

## Ver el Historial de Commits

```bash
git log
```

Para ver un resumen corto en una sola línea por commit:

```bash
git log --oneline
```

---

## Editar el Último Commit

Si te equivocaste en el mensaje del commit más reciente, puedes cambiarlo:

```bash
git commit --amend -m "Nuevo mensaje"
```

⚠️ El identificador (`hash`) del commit **cambiará**.

---

## Ignorar Archivos

Algunos archivos **no deberían subirse** al repositorio remoto, por ejemplo: `.env`, archivos de configuración local, etc.

Usa un archivo `.gitignore` para excluirlos. Ejemplo de `.gitignore`:

```
.env
node_modules/
*.log
```

---

## ¿Qué es el HEAD?

`HEAD` es un **puntero** que indica dónde estás actualmente en el repositorio.

- Con `git log --oneline` verás algo como:
  ```
  a1b2c3d (HEAD -> main) mensaje del commit
  ```

Esto indica que estás en la rama `main` y en el commit `a1b2c3d`.

---

## Resumen de Comandos Útiles

| Comando                          | Descripción                                      |
|----------------------------------|--------------------------------------------------|
| `git status`                    | Ver archivos modificados y estado actual        |
| `git add nombreArchivo`         | Añadir archivo al área de staging               |
| `git add .`                     | Añadir todos los archivos modificados           |
| `git commit -m "mensaje"`       | Hacer un commit con mensaje                     |
| `git restore --staged archivo`  | Quitar archivo del área de staging              |
| `git log`                       | Ver historial de commits                        |
| `git log --oneline`             | Ver historial resumido                          |
| `git commit --amend -m "nuevo"` | Cambiar mensaje del último commit               |


# Ramas, Merge y Conflictos

---
### ¿Qué es una Rama?
Una rama es una bifurcación de donde estamos en Git. A nivel técnico, es un **apuntador hacia nuevas confirmaciones**.

### ¿Para qué sirven las Ramas?
Permiten trabajo colaborativo, donde cada persona puede trabajar en una línea diferente del proyecto.

### 📌 Comandos para trabajar con Ramas
```bash
git branch nombreRama         # Crea una nueva rama
git switch nombreRama         # Cambia a una rama existente
git switch -c nombreRama      # Crea y cambia a la rama
```

### Fusionar Ramas
Fusionar significa integrar los cambios de una rama a otra:
```bash
git merge nombreRama
```

### Conflictos en Git
Un conflicto ocurre cuando Git **no puede determinar automáticamente qué cambio debe conservarse** al fusionar.

#### Resolviendo conflictos (formato del archivo)
```diff
<<<<<<< HEAD
<p>Contenido actual</p>
=======
<p>Contenido nuevo</p>
>>>>>>> changes
```

El usuario debe elegir qué contenido conservar o combinar ambos.

# GitHub, push, pull y pull-request 

---
### ¿Git y GitHub son lo mismo?
- **Git**: Control de versiones
- **GitHub**: Plataforma para alojar código basado en Git

### Alternativas a GitHub
- BitBucket
- GitLab

### ¿ Qué son los repositorios Remotos?
Son puntos de sincronización entre repositorios locales.

#### Enlazar repositorio local con remoto:
```bash
git remote add origin urlRepositorio
```

### Generar clave SSH
Sirve para autenticación segura.

Se realiza mediante el siguiente comando:

```bash
git config list   # Ver configuración actual
```

### Clonar repositorio
```bash
git clone urlRepositorio
```

### Subir cambios
```bash
git push origin nombreRama     # Enviar ramas locales a un repositorio remoto
git branch -a                  # Ver ramas locales y remotas
```

### Eliminar ramas
```bash
git remote prune origin        # Eliminar ramas remotas que ya no existen
```

### Git Push vs Git Pull
- `git push`: Sube cambios del local al remoto
- `git pull`: Trae cambios del remoto al local

### Comandos Git Push
```bash
git fetch                          # Actualiza referencias
git push -u origin <rama>
git push origin <rama1><rama2><rama3> # Muestra solo las ramas listadas
git push -d origin <rama>          # Borra rama remota
git push -f                        # Forzar subida
```

### 📥 Pull Request (PR)
Petición para fusionar cambios del local al original.

#### Hacer una PR
1. Desde la rama en GitHub → botón para crear PR
2. Desde pestaña Pull Request

#### Buena PR
- Código hace una sola cosa
- Explicación clara
- Usa imágenes si es necesario

#### Revisar PR
- Feedback claro y específico
- Entender el contexto

---

