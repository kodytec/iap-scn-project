# Sistema de Control de Notas (SCN)

**Curso:** Introducción a la Programación con Python (IAP)  
**Autor:** Kodytec  

## Descripción del Proyecto

El proyecto **Sistema de Control de Notas (SCN)** es una aplicación diseñada para gestionar la información académica y financiera de los alumnos de un curso. Esta aplicación permitirá a los alumnos iniciar sesión, visualizar los cursos en los que están inscritos, gestionar sus pagos y realizar nuevos pagos.

### Funcionalidades Principales

1. **[Inicio de sesión](#inicio-de-sesión):**  
   Permitir a los alumnos autenticarse en el sistema utilizando sus credenciales.

2. **[Listado de cursos](#funcionalidad-detallada-listado-de-cursos):**  
   Mostrar los cursos en los que el alumno está inscrito, permitiendo filtrar por estado (aprobado o desaprobado) y ordenar por nota.

3. **[Listado de pagos](#listado-de-pagos):**  
   Mostrar los pagos realizados por el alumno, con la posibilidad de ver el historial completo.

4. **[Realizar pago](#realizar-pago):**  
   Permitir a los alumnos realizar pagos pendientes directamente desde la aplicación.

---

## Funcionalidad Detallada: Listado de Cursos

### Descripción General

Desarrollar una función en Python que permita listar los cursos en los que está inscrito un alumno específico, con la capacidad de filtrar los cursos por su estado (aprobado o desaprobado) y ordenar los resultados de mayor a menor nota.

### Detalle de la Funcionalidad

- **Función:** `listarCursosPorAlumno(codigoAlumno: str, estado: str, ordenarPorNota: bool) -> list[dict]`
  
  - **Parámetros:**
    - `codigoAlumno` (str): Código único del alumno.
    - `estado` (str): Estado del curso a filtrar. Puede ser "aprobado", "desaprobado" o "todos".
    - `ordenarPorNota` (bool): Determina si los cursos se ordenan de mayor a menor nota (`True`/`False`).

  - **Salida:**
    Una lista de diccionarios que contiene la información de los cursos:
    - `id` (str): Identificador único del curso.
    - `nombreCurso` (str): Nombre del curso.
    - `nota` (float): Nota obtenida en el curso.
    - `grado` (str): Grado en el que se imparte el curso.
    - `profesor` (str): Nombre del profesor que imparte el curso.
    - `estado` (str): Estado de aprobación del curso ("aprobado" o "desaprobado").

### Criterios de Aceptación

1. La función debe devolver una lista de cursos filtrados correctamente por el estado solicitado.
2. Los cursos deben ordenarse de mayor a menor nota si el parámetro `ordenarPorNota` es `True`.
3. La lista devuelta debe contener los campos especificados (`id`, `nombreCurso`, `nota`, `grado`, `profesor`, `estado`).
4. Si no hay cursos que coincidan con los criterios de búsqueda, la función debe devolver una lista vacía.

### Casos de Prueba y Resultados Esperados

Dado el siguiente diccionario de datos de ejemplo:

```python
cursos = [
    {'id': 'C101', 'nombreCurso': 'Matemáticas', 'nota': 18.5, 'grado': '5to', 'profesor': 'Renzo Santillán', 'estado': 'aprobado'},
    {'id': 'C102', 'nombreCurso': 'Ciencias', 'nota': 16.0, 'grado': '5to', 'profesor': 'Pamela Vinazza', 'estado': 'aprobado'},
    {'id': 'C103', 'nombreCurso': 'Historia', 'nota': 9.0, 'grado': '5to', 'profesor': 'Joel Campos', 'estado': 'desaprobado'}
]
```

| **Caso de Prueba**                               | **Descripción**                                                                                           | **Resultado Esperado**                                                                                                                                               |
|--------------------------------------------------|-----------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `listarCursosPorAlumno('C1', 'aprobado', True)`  | Filtra los cursos aprobados del alumno con código 'C1' y los ordena de mayor a menor nota.                 | `[{'id': 'C101', 'nombreCurso': 'Matemáticas', 'nota': 18.5, 'grado': '5to', 'profesor': 'Renzo Santillán', 'estado': 'aprobado'}, {'id': 'C102', 'nombreCurso': 'Ciencias', 'nota': 16.0, 'grado': '5to', 'profesor': 'Pamela Vinazza', 'estado': 'aprobado'}]` |
| `listarCursosPorAlumno('C1', 'desaprobado', False)` | Filtra los cursos desaprobados del alumno con código 'C1' sin ordenar por nota.                             | `[{'id': 'C103', 'nombreCurso': 'Historia', 'nota': 9.0, 'grado': '5to', 'profesor': 'Joel Campos', 'estado': 'desaprobado'}]`                                                                               |
| `listarCursosPorAlumno('C1', 'todos', True)`       | Muestra todos los cursos del alumno con código 'C1' y los ordena de mayor a menor nota.                    | `[{'id': 'C101', 'nombreCurso': 'Matemáticas', 'nota': 18.5, 'grado': '5to', 'profesor': 'Renzo Santillán', 'estado': 'aprobado'}, {'id': 'C102', 'nombreCurso': 'Ciencias', 'nota': 16.0, 'grado': '5to', 'profesor': 'Pamela Vinazza', 'estado': 'aprobado'}, {'id': 'C103', 'nombreCurso': 'Historia', 'nota': 9.0, 'grado': '5to', 'profesor': 'Joel Campos', 'estado': 'desaprobado'}]` |
| `listarCursosPorAlumno('C2', 'aprobado', True)`    | Filtra los cursos aprobados del alumno con código 'C2' y los ordena de mayor a menor nota.                  | `[]` (Lista vacía si el alumno no tiene cursos que coincidan con los criterios de búsqueda).                                                                          |

---

## A cerca de

Este proyecto es parte del curso **Introducción a la Programación con Python (IAP)** ofrecido por **Kodytec**.  
Para más información sobre el curso y otros proyectos, visita nuestro sitio web https://kodytec.pe o contáctanos directamente al +51 968491916.  
**Kodytec** se compromete a brindar educación de calidad en el campo de la programación y tecnología a colegios nacionales y particulares.

---
