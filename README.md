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
   👉 Se detectan con:  
   ```bash
   git status
   ```

2. **STAGED**  
   El archivo ha sido **marcado como preparado para ser confirmado** en el repositorio local.  
   👉 Para mover un archivo a este estado:  
   ```bash
   git add nombreArchivo
   ```
   👉 Para agregar todos los archivos modificados:  
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

Si agregaste un archivo por error al `staging`, puedes deshacerlo con:

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

---

