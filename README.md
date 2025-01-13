# Workshop: Uso de Git y GitHub para Colaboración en Equipo

## **Objetivo del taller**
Este workshop está diseñado para enseñar a dos personas cómo colaborar en un proyecto utilizando Git y GitHub. A lo largo de este taller, aprenderán los conceptos básicos de Git, cómo trabajar con ramas, resolver conflictos, gestionar issues y realizar pull requests.

## **Requisitos previos**
- Tener Git instalado en tu ordenador.
- Tener una cuenta activa en GitHub.
- Un editor de texto o IDE instalado (por ejemplo, VS Code).

---

## **Parte 1: Configuración Inicial**

### 1. Configurar Git localmente
En este paso configuraremos Git con tu nombre y correo electrónico para que todos los cambios que realices se asocien correctamente a tu identidad.

1. Abre tu terminal o línea de comandos.
2. Configura tu nombre y correo electrónico:
    ```bash
    git config --global user.name "Tu Nombre"
    git config --global user.email "tuemail@example.com"
    ```
3. Verifica la configuración:
    ```bash
    git config --list
    ```

### 2. Crear un repositorio en GitHub
En este paso, una de las personas del equipo creará el repositorio remoto donde se almacenará el proyecto.

1. Una persona del equipo debe:
    - Iniciar sesión en GitHub.
    - Crear un nuevo repositorio llamado `proyecto-colaborativo`.
    - Configurar el repositorio como público o privado.
2. Copiar la URL del repositorio (por ejemplo, `https://github.com/usuario/proyecto-colaborativo.git`).

### 3. Clonar el repositorio
Ambas personas deben clonar el repositorio en sus ordenadores para empezar a trabajar en el proyecto de forma colaborativa.

1. Ambas personas deben clonar el repositorio en su ordenador:
    ```bash
    git clone https://github.com/usuario/proyecto-colaborativo.git
    ```
2. Navegar al directorio del proyecto:
    ```bash
    cd proyecto-colaborativo
    ```

---

## **Parte 2: Primeros pasos con Git**

### **Objetivo**
En esta sección, aprenderemos a crear, modificar y sincronizar archivos en un repositorio compartido. Comenzaremos con tareas simples, sin conflictos, y luego exploraremos cómo resolver un conflicto.

### 1. Crear y modificar archivos

1. Ambas personas deben crear archivos con nombres diferentes para evitar conflictos iniciales:
    - **Persona 1:** Crear un archivo llamado `archivo1.md` con este contenido:
      ```markdown
      # Archivo 1

      Contenido inicial escrito por Persona 1.
      ```
      Comandos:
      ```bash
      echo "# Archivo 1\n\nContenido inicial escrito por Persona 1." > archivo1.md
      git add archivo1.md
      git commit -m "Añadir archivo1.md con contenido inicial (Persona 1)"
      ```
    - **Persona 2:** Crear un archivo llamado `archivo2.md` con este contenido:
      ```markdown
      # Archivo 2

      Contenido inicial escrito por Persona 2.
      ```
      Comandos:
      ```bash
      echo "# Archivo 2\n\nContenido inicial escrito por Persona 2." > archivo2.md
      git add archivo2.md
      git commit -m "Añadir archivo2.md con contenido inicial (Persona 2)"
      ```

2. **Sincronizar los cambios con el repositorio remoto:**
    - Persona 1 debe enviar sus cambios:
      ```bash
      git push origin main
      ```
    - Persona 2 debe actualizar su copia local y luego enviar sus cambios:
      ```bash
      git pull origin main
      git push origin main
      ```
    - Ambas personas deben verificar que tienen los cambios del otro:
      ```bash
      git pull origin main
      ```

### 2. Generar y resolver un conflicto

Los conflictos ocurren cuando dos personas modifican la misma parte de un archivo al mismo tiempo. En este paso aprenderemos a resolverlos.

1. Ambas personas deben editar el archivo `archivo1.md` al mismo tiempo:
    - **Persona 1:** Añadir esta línea al final:
      ```markdown
      Línea añadida por Persona 1.
      ```
      Comandos:
      ```bash
      echo "Línea añadida por Persona 1." >> archivo1.md
      git add archivo1.md
      git commit -m "Añadir línea en archivo1.md (Persona 1)"
      git push origin main
      ```
    - **Persona 2:** Añadir esta línea al final:
      ```markdown
      Línea añadida por Persona 2.
      ```
      Comandos:
      ```bash
      echo "Línea añadida por Persona 2." >> archivo1.md
      git add archivo1.md
      git commit -m "Añadir línea en archivo1.md (Persona 2)"
      git push origin main
      ```

2. **Resolución del conflicto:**
    - Persona 2 recibirá un error al intentar hacer `push`. Debe actualizar su copia local y resolver el conflicto:
      ```bash
      git pull origin main
      ```
    - Git marcará el conflicto en `archivo1.md`. Persona 2 debe abrir el archivo y resolverlo, dejando ambos cambios:
      ```markdown
      # Archivo 1

      Contenido inicial escrito por Persona 1.

      Línea añadida por Persona 1.
      Línea añadida por Persona 2.
      ```
    - Persona 2 debe guardar el archivo, añadirlo al área de preparación y hacer un nuevo commit:
      ```bash
      git add archivo1.md
      git commit -m "Resolver conflicto en archivo1.md"
      git push origin main
      ```

3. **Actualizar la copia local:**
    - Persona 1 debe actualizar su copia local para obtener los cambios:
      ```bash
      git pull origin main
      ```

### 3. Verificar el estado del repositorio
El comando `git status` permite verificar el estado de los archivos antes y después de realizar cambios. Ambas personas deben utilizarlo frecuentemente:
    ```bash
    git status
    ```
Este comando muestra información sobre los archivos modificados, añadidos y pendientes de commit.

---

## **Parte 3: Uso de ramas para nuevas funcionalidades**

### **Objetivo**
Las ramas permiten trabajar en nuevas funcionalidades sin afectar el código principal. Son útiles para trabajar en paralelo y probar cambios antes de integrarlos en la rama principal.

### 1. Crear y trabajar en una rama

1. Una persona debe:
    - Crear una nueva rama llamada `feature-texto`:
      ```bash
      git checkout -b feature-texto
      ```
    - Crear un archivo `texto.md` con el siguiente contenido:
      ```markdown
      ## Nuevo archivo

      Este es un archivo de ejemplo para practicar con ramas.
      ```
    - Guardar el archivo y hacer un commit:
      ```bash
      git add texto.md
      git commit -m "Añadir archivo texto.md en la rama feature-texto"
      ```
    - Subir la rama al repositorio remoto:
      ```bash
      git push origin feature-texto
      ```

### 2. Revisar y fusionar la rama

1. La otra persona debe:
    - Ir al repositorio en GitHub.
    - Abrir un Pull Request (PR) desde la rama `feature-texto` hacia `main`.
    - Revisar los cambios, añadir un comentario y aprobar el PR.
2. La persona que creó la rama debe fusionar el PR y eliminar la rama:
    - En GitHub, seleccionar "Merge pull request" y luego "Delete branch".

### 3. Actualizar el repositorio local

1. Ambas personas deben actualizar sus repositorios locales para obtener los cambios:
    ```bash
    git pull origin main
    ```

---

## **Parte 4: Gestión de Issues**

### **Objetivo**
Los issues son herramientas en GitHub para rastrear tareas, errores o ideas. Son esenciales para coordinar el trabajo en equipo y documentar lo que se debe hacer.

### 1. Crear un issue

1. Una persona debe:
    - Ir a la pestaña "Issues" en GitHub.
    - Crear un nuevo issue con el título: "Añadir información al archivo texto.md".
    - Asignar el issue a la otra persona.

### 2. Resolver el issue

1. La persona asignada debe:
    - Crear una nueva rama para trabajar en el issue:
      ```bash
      git checkout -b fix-texto
      ```
    - Editar el archivo `texto.md` añadiendo más contenido:
      ```markdown
      ## Nuevo archivo

      Este es un archivo de ejemplo para practicar con ramas.

      Ahora contiene más información para probar la gestión de issues.
      ```
    - Guardar los cambios, hacer un commit y subir la rama:
      ```bash
      git add texto.md
      git commit -m "Actualizar archivo texto.md con más contenido"
      git push origin fix-texto
      ```

### 3. Cerrar el issue

1. Crear un PR desde la rama `fix-texto` y referenciar el issue en el mensaje (por ejemplo, "Closes #1").
2. Revisar, aprobar y fusionar el PR como en el paso anterior.
3. Verificar que el issue se cierre automáticamente.

---

## **Parte 5: Resolución de conflictos**

### 1. Generar un conflicto

1. Ambas personas deben editar el archivo `texto.md` en la rama `main` al mismo tiempo.
    - Persona 1: Añadir "Línea A" al final del archivo.
    - Persona 2: Añadir "Línea B" al final del archivo.
    - Ambas deben hacer commit y push:
      ```bash
      git add texto.md
      git commit -m "Añadir Línea A (o B)"
      git push origin main
      ```

### 2. Resolver el conflicto

1. La segunda persona que haga el push recibirá un error. Debe realizar un pull para resolver el conflicto:
    ```bash
    git pull origin main
    ```
2. Git marcará el conflicto en el archivo `texto.md`. Abrir el archivo y resolverlo, dejando ambos cambios:
    ```markdown
    ## Nuevo archivo

    Este es un archivo de ejemplo para practicar con ramas.

    Ahora contiene más información para probar la gestión de issues.

    Línea A
    Línea B
    ```
3. Hacer un commit para resolver el conflicto:
    ```bash
    git add texto.md
    git commit -m "Resolver conflicto en texto.md"
    git push origin main
    ```

---

## **Parte 6: Finalización del taller**

¡Enhorabuena! Ahora sabes cómo:
- Configurar y usar Git y GitHub.
- Trabajar con ramas y Pull Requests.
- Gestionar issues.
- Resolver conflictos.

Practica regularmente para consolidar estos conocimientos. 🎉
