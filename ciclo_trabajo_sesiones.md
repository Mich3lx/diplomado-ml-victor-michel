# 🔄 Ciclo de Trabajo por Sesión — Diplomado ML en Seguros

**Facultad de Ciencias, UNAM · Módulo 1: Introducción a Python**

---

## Panorama General

```
┌─────────────────────────────────────────────────────────────────────┐
│                         GITHUB (nube)                               │
│                                                                     │
│   📦 diplomado-ml-seguros        📦 diplomado-ml-TuNombre           │
│      (Repo del INSTRUCTOR)          (Repo del ALUMNO)               │
│             ↑                               ↑                       │
│         git push                        git push                    │
│             │                               │                       │
│    [PC Eric - instructor]         [PC Alumno]                       │
│                                                                     │
│    Los alumnos hacen git pull     Solo el alumno sube aquí          │
│    para bajar el material         Eric solo lee / revisa            │
└─────────────────────────────────────────────────────────────────────┘
```

---

## 📋 Regla de Oro

```
┌──────────────────────────────────────────────────────────────────┐
│                                                                  │
│   diplomado-ml-seguros    →   solo git pull  (bajar material)    │
│                                                                  │
│   diplomado-ml-TuNombre   →   git add · commit · push           │
│                                  (subir ejercicios)              │
│                                                                  │
└──────────────────────────────────────────────────────────────────┘
```

---
## Estrutura general

```
📁 ESTRUCTURA QUE DEBES TENER ANTES DE SUBIR
─────────────────────────────────────────────
diplomado-ml-seguros\
└── modulo1\
    ├── sesion4\
    │   ├── sesion4_M1_slides.pptx     ✅ ya subido
    │   └── sesion4_M1_notebook.ipynb  ✅ ya subido
    └── sesion5\                       ← NUEVO
        ├── sesion5_M1_slides.pptx
        └── sesion5_M1_notebook.ipynb
```

**1. Abre una nueva terminal desde la carpeta donde estas parado en VS code (Terminal: Create new terminal)**

Aqui verifica tu ruta de trabajo con dir:

```bash
"C:\Users\Eric_Daniel\Documents\Ciencias Cursos\Diplomado"
```

Debes tener una carpeta que contenga a las dos careptas: **(cd nombredelacarpeta)**

```bash
cd "C:\Users\Eric_Daniel\Documents\Ciencias Cursos\Diplomado\diplomado-ml-seguros"
```
Contiene verifca con dir:

Curso:
```bash
cd "C:\Users\Eric_Daniel\Documents\Ciencias Cursos\Diplomado\diplomado-ml-seguros\diplomado-ml-seguros"
```

Propia:

```bash
cd "C:\Users\Eric_Daniel\Documents\Ciencias Cursos\Diplomado\diplomado-ml-seguros\diplomado-ml-eric-demo"
```

Dependiendo de que la carpeta será lo que tengamos que hacer:

## PARTE 1 — Carpeta del curso


### Instructor o propetario:

> **Quién:** Eric/Eduardo/Karla
> **Cuándo:** Antes de la sesión (idealmente la noche anterior)  
> **Dónde:** Carpeta `diplomado-ml-seguros`


**1. Se validan los cambios**

```bash
git status
# Debe mostrar los archivos nuevos de la sesión 5 en rojo
```

**2. Se actualiza en la nube**
```bash
git add .

git commit -m "Agrega material sesion 5: funciones avanzadas y modulos"

git push
```

**4. Verifica en GitHub:**

```
Abre: github.com/TuUsuario/diplomado-ml-seguros
Debes ver la carpeta modulo1/sesion5 con los archivos nuevos
```

```
✅ LISTO — Los alumnos ya pueden descargar el material
```

---

### Alumno:

> **Quién:** Cada alumno  
> **Cuándo:** Antes de clase o al inicio de la sesión  
> **Dónde:** Carpeta `diplomado-ml-seguros` (repo del instructor)


**1. Ve a la carpeta que descragaste del instructor la que se tuvo que generar al hacer el clone**

```bash
cd "C:\Users\TuNombre\Documents\diplomado-ml-seguros"
```

> 💡 La ruta depende de dónde clonaron el repo. Si no la recuerdas:
> abre el Explorador de Windows, busca la carpeta `diplomado-ml-seguros`,
> clic derecho → "Copiar como ruta"

**2. Descarga el material nuevo:**

```bash
git pull
```

**3. Verifica que llegó el material:**

```bash
dir modulo1\sesion5
# Debe mostrar los archivos de la sesión 5
```

```
✅ LISTO — Tienes el material de la sesión 5 en tu computadora
```

```
⚠️  IMPORTANTE
────────────────────────────────────────────────────────
NO modifiques archivos dentro de diplomado-ml-seguros.
Esta carpeta es solo para descargar — nunca subas nada aquí.
Si editaste algo por accidente, ejecuta: git restore .
────────────────────────────────────────────────────────
```

---

## PARTE 2 - Carpeta del alumno (Para subir tareas)

> **Quién:** Cada alumno  
> **Cuándo:** Durante o después de clase  
> **Dónde:** Carpeta `diplomado-ml-TuNombre` (TU repo)

### Paso a paso

**1. Copia el notebook de ejercicio al TU repo**

**Método A — Explorador de Windows (recomendado):**

```
1. Abre el Explorador de Windows
2. Navega a:
   diplomado-ml-seguros\modulo1\sesion5\
3. Copia el archivo:
   sesion5_M1_notebook.ipynb
4. Navega a TU carpeta:
   diplomado-ml-TuNombre\modulo1\sesion5\
   (crea la carpeta sesion5 si no existe)
5. Pega el archivo y renómbralo:
   sesion5_ejercicio_TuNombre.ipynb
```

**Método B — Desde la terminal:**

```bash
# Crear la carpeta si no existe
mkdir "C:\Users\TuNombre\Documents\diplomado-ml-TuNombre\modulo1\sesion5"

# Copiar el archivo
copy "C:\Users\TuNombre\Documents\diplomado-ml-seguros\modulo1\sesion5\sesion5_M1_notebook.ipynb" ^
     "C:\Users\TuNombre\Documents\diplomado-ml-TuNombre\modulo1\sesion5\sesion5_ejercicio_TuNombre.ipynb"
```

> 💡 El símbolo `^` permite partir el comando en dos líneas en Windows.
> En Mac/Linux usa `\` en lugar de `^` y cambia `copy` por `cp`.

**2. Resuelve el ejercicio en Jupyter / VS Code**

```
Abre VS Code → File → Open Folder → selecciona diplomado-ml-TuNombre
Abre el notebook sesion5_ejercicio_TuNombre.ipynb
Resuelve las tareas
Guarda el archivo (Ctrl+S)
```

**3. Navega a TU repo en la terminal:**

```bash
cd "C:\Users\TuNombre\Documents\diplomado-ml-TuNombre"
```

**4. Verifica qué archivos cambiaron:**

```bash
git status
# Debe aparecer en rojo:
# modulo1/sesion5/sesion5_ejercicio_TuNombre.ipynb
```

**5. Agrega los cambios:**

```bash
git add .
```

> ⚠️ Si aparece este mensaje, **no es un error — ignóralo y continúa:**
> ```
> warning: LF will be replaced by CRLF the next time Git touches it
> ```

**6. Crea el commit:**

```bash
git commit -m "Sesion 5: ejercicio de funciones avanzadas completado"
```

> 💡 **Buenos mensajes de commit:**
> ```
> ✅  "Sesion 5: ejercicio completado"
> ✅  "Sesion 5: agrego funciones calcular_prima y evaluar_poliza"
> ❌  "cambios"
> ❌  "hola"
> ❌  "asdf"
> ```

**7. Sube a GitHub:**

```bash
git push
```

**8. Verifica que se subió:**

```
Abre tu navegador y ve a:
github.com/TuUsuario/diplomado-ml-TuNombre

Debes ver la carpeta modulo1/sesion5 con tu notebook
```

```
✅ LISTO — El instructor puede ver tu ejercicio en GitHub
```

---

## Resumen Visual del Ciclo Completo

```
INSTRUCTOR (Eric)                    ALUMNOS
─────────────────                    ──────────────────────────────────────

1. Prepara material                  
   sesion5_slides.pptx               
   sesion5_notebook.ipynb            
         │                           
2. Sube a GitHub                     
   git add .                         
   git commit -m "Sesion 5"          
   git push                          
         │                           
         ▼                           
   📦 diplomado-ml-seguros           
      (GitHub - nube)                
         │                           
         │                    3. Descargan material nuevo
         │                       cd diplomado-ml-seguros
         └──────────────────►       git pull
                                       │
                                4. Copian el notebook
                                   a SU propia carpeta
                                   y lo renombran
                                       │
                                5. Resuelven el ejercicio
                                   en Jupyter / VS Code
                                       │
                                6. Suben su trabajo
                                   cd diplomado-ml-TuNombre
                                   git add .
                                   git commit -m "Sesion 5"
                                   git push
                                       │
                                       ▼
                              📦 diplomado-ml-TuNombre
                                 (GitHub - nube)
                                       │
         ◄─────────────────────────────┘
7. Eric revisa
   github.com/alumno/diplomado-ml-TuNombre
   (sin descargar nada)
```

---

## Errores Comunes y Soluciones

```
┌────────────────────────────────────────────────────────────────────────────┐
│ ERROR                          │ CAUSA              │ SOLUCIÓN             │
├────────────────────────────────────────────────────────────────────────────┤
│ warning: LF will be replaced   │ Normal en Windows  │ Ignorar, continuar   │
│                                │                    │                      │
│ fatal: not a git repository    │ Carpeta equivocada │ cd a la carpeta      │
│                                │                    │ correcta             │
│                                │                    │                      │
│ error: failed to push          │ Hay cambios en     │ git pull primero     │
│                                │ GitHub que no      │ luego git push       │
│                                │ tienes local       │                      │
│                                │                    │                      │
│ Authentication failed          │ Token expirado     │ Genera nuevo PAT en  │
│                                │                    │ GitHub → Settings    │
│                                │                    │ → Developer settings │
│                                │                    │ → Tokens             │
└────────────────────────────────────────────────────────────────────────────┘
```

---

## Estructura Final de Carpetas (referencia)

```
📁 diplomado-ml-seguros\              ← REPO INSTRUCTOR (solo leer)
│   modulo1\
│   ├── sesion1\
│   │   └── sesion1_M1_notebook.ipynb
│   ├── sesion2\
│   │   └── sesion2_M1_notebook.ipynb
│   ├── sesion3\
│   │   └── sesion3_M1_notebook.ipynb
│   ├── sesion4\
│   │   └── sesion4_M1_notebook.ipynb
│   └── sesion5\                      ← nuevo esta semana
│       └── sesion5_M1_notebook.ipynb

📁 diplomado-ml-TuNombre\             ← TU REPO (aquí trabajas)
│   modulo1\
│   ├── sesion1\
│   │   └── sesion1_ejercicio_TuNombre.ipynb
│   ├── sesion2\
│   │   └── sesion2_ejercicio_TuNombre.ipynb
│   ├── sesion3\
│   │   └── sesion3_ejercicio_TuNombre.ipynb
│   ├── sesion4\
│   │   └── sesion4_ejercicio_TuNombre.ipynb
│   └── sesion5\                      ← copias aquí y resuelves
│       └── sesion5_ejercicio_TuNombre.ipynb
│   tareas\
│   └── tarea1_TuNombre.ipynb
```

---

*Diplomado ML en Seguros · Facultad de Ciencias, UNAM · 2026*
