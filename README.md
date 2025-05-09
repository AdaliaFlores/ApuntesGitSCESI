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

# Flujos de Trabajo en Git

---

## GitFlow

Modelo clásico orientado a equipos grandes y proyectos con despliegues planificados.

- `main`: Código en producción
- `develop`: Código listo para pruebas
- `feature`: Nuevas funcionalidades
- `release`: Cambios finales
- `hotfix`: Arreglos rápidos

> Ideal para: ciclos de lanzamiento largos, software empresarial, múltiples entornos (dev, staging, prod).

---

## GitHub Flow

- Solo dos tipos de ramas principales: `main` + ramas de trabajo.
- Las ramas de trabajo nacen desde `main` y se **fusionan mediante Pull Requests**.
- Se corre CI/CD automáticamente al abrir la PR.

> Ideal para: despliegue continuo, proyectos open source, equipos ágiles.

---

## Trunk-Based Development


- Solo existe la rama `main`, y ramas **efímeras** que duran pocas horas o días.
- Todo cambio se fusiona a `main` rápidamente (con revisiones mínimas).
- Imprescindible usar **CI/CD, testing automatizado y feature flags**.

> Ideal para: startups, despliegues diarios, equipos avanzados.

---

## Ship / Show / Ask

Modelo basado en la **confianza y seguridad del desarrollador**:

- **Ship**: El código se fusiona directamente a `main`, **sin revisión**.  
    Se usa cuando estás **100% seguro** de tu cambio.

- **Show**: Se crea un PR que puede ser revisado, pero **no bloquea la fusión**.  
    Útil cuando estás **seguro (80%)** y solo quieres compartirlo.

- **Ask**: Se crea un PR que **debe ser aprobado** antes de fusionar.  
     Para cuando necesitas **feedback o validación**.

> Ideal para: flujos colaborativos y desarrollo transparente.

# Buenas Prácticas en Git

---

### ¿Por qué son importantes las buenas prácticas?

Aplicar buenas prácticas en Git no solo mantiene el proyecto organizado, sino que también:

- Facilita la colaboración en equipos pequeños o grandes.
- Mejora la legibilidad del historial de cambios.
- Hace más fácil identificar errores o cambios específicos.
- Reduce conflictos al fusionar ramas.

---

### ¿Cada cuánto hacer commits?

**Haz commits pequeños, frecuentes y significativos**

- Un commit por cada cambio lógico: **no mezcles correcciones con nuevas funcionalidades**.
- Evita commits enormes que incluyan múltiples cosas (difíciles de revisar y deshacer).


---

### Escribir buenos mensajes de commit
- Usa verbo imperativo (add, fix, change, etc.)
- Sin punto final
- En minúsculas
- Mínimo 50 caracteres de contexto

### Tipos de Commits
| Tipo     | Descripción                                 |
|----------|---------------------------------------------|
| feat     | Nueva funcionalidad                         |
| fix      | Corrección de bug                           |
| perf     | Mejora de rendimiento                       |
| build    | Cambios en sistema de build                 |
| ci       | Cambios de integración continua             |
| docs     | Documentación                               |
| refactor | Refactorización                             |
| style    | Cambios de estilo                           |
| test     | Nuevos tests o refactor de existentes       |

Ejemplo:
```bash
feat(backend): add filter for cars
```

### Nombres de ramas
- Usa nombres consistentes
- Refleja la acción que se realiza

# Deshacer Cambios

---

### ¿Cuándo deshacer?
- Falló el proyecto
- Eliminar cambios
- Recuperar archivos

### Comandos destructivos vs no destructivos
- **Destructivos**: Afectan el historial
- **No destructivos**: Mantienen historial

### Git Reset
- se usa para mover el puntero `HEAD` a otro commit. Afecta el historial y el área de trabajo según el modo que elijas.

```bash
git reset --soft <SHA> 
git reset --hard <SHA>
git reset --hard HEAD~N
git reset --soft HEAD~N
```

### Git Revert
-  revierte los efectos de un commit creando un nuevo commit inverso. No borra historial.

```bash
git revert <SHA>
git revert HEAD~N
git revert --abort
```

### Git Checkout
-  permite moverse a diferentes commits, ramas o archivos.

```bash
git checkout <SHA>
git checkout HEAD~N
```

### Ver qué se hizo
```bash
git show <SHA>
```

### Recuperar si borraste todo

```bash
git log #Busca el commit al que deseas regresar o revisar.
git pull origin #Descarga los cambios más recientes del repositorio remoto.
```
## Otra solucion

```bash
git reflog #Muestra el historial de movimientos de HEAD, incluso después de un reset --hard.
git revert hard #para recuperar

```
## EXTRA:
para ver que hicimos en algún archivo ponemos: 

```bash
git show identficadorCommit
```
# Hooks, Alias y Trucos de Git
---

### ¿Qué es un Hook?
Scripts que se ejecutan en eventos específicos de Git.

#### Hooks del lado del cliente:
- `pre-commit`: Validar antes de hacer commit
- `prepare-commit-msg`: Modificar mensaje
- `commit-msg`: Validar el mensaje
- `post-commit`: Notificaciones
- `pre-push`: Ejecutar tests
- `post-checkout`, `post-merge`: Limpieza

#### Hooks del servidor:
- `update`: Validar actualizaciones
- `pre-receive`: Verificar antes de grabar
- `post-receive`: Enviar notificaciones

#### Crear un hook:
Archivo en `.git/hooks/nombre-hook`

### Alias de Git
```bash
git config --global alias.co checkout
```

### Trucos de Git

#### Guardar cambios temporalmente
```bash
git stash
git stash -u
git stash pop
git stash clear
```

#### Aplicar commits específicos
```bash
git cherry-pick <SHA>
```

#### Buscar commit que introduce un bug
```bash
git bisect start
git bisect bad
git bisect good
git bisect reset
```

#### Recuperar archivo específico
```bash
git checkout <SHA> <archivo>
```

---
