# Sistema de Control de Notas (SCN)

**Curso:** Introducción a la Programación con Python (IAP)  
**Autor:** Kodytec  

## Descripción del Proyecto

El proyecto **Sistema de Control de Notas (SCN)** es una aplicación (Web y Mobile) diseñada para gestionar la información académica y financiera de los alumnos de un curso. Esta aplicación permitirá a los alumnos iniciar sesión, visualizar los cursos en los que están inscritos y gestionar sus pagos.

### Funcionalidades Principales

1. **[Inicio de sesión](#inicio-de-sesión):**  
   Permitir a los alumnos autenticarse en el sistema utilizando sus credenciales.

2. **[Listar cursos](#listar-cursos):**  
   Mostrar los cursos en los que el alumno está inscrito, permitiendo filtrar por estado (aprobado o desaprobado) y ordenar por nota.

3. **[Listar pagos](#listar-pagos):**  
   Mostrar los pagos realizados por el alumno, con la posibilidad de ver el historial completo.

4. **[Obtener descuento](#obtener-descuento):**  
   Calcula el descuento de un alumno según su categoría y el concepto de pago.
   
5. **[Pagar](#pagar):**  
   Permitir a los alumnos realizar pagos pendientes directamente desde la aplicación.

---
## Inicio de Sesión
---

### Descripción General

Desarrollar una función en Python que permita a los alumnos iniciar sesión en el sistema verificando su código de alumno y clave.

### Detalle de la Funcionalidad

- **Nombre de la función:** `inicioSesion(codigo, clave)`

  - **Parámetros:**
    - `codigo` (str): Código de alumno que intenta iniciar sesión.
    - `clave` (str): Clave proporcionada por el alumno.

  - **Salida:**
    - Un mensaje (str):
       1. `"Usuario no encontrado"` si el usuario no existe.
       1. `"Clave incorrecta"` si la clave es incorrecta o no cumple con los criterios.
       1. `"Inicio de sesión exitoso. Bienvenido [NOMBRE]"`, en caso de éxito.

### Criterios de Aceptación

1. La función debe verificar si el alumno existe en el diccionario de alumnos.
2. Si el alumno existe, la función debe comprobar que la clave proporcionada coincida con la almacenada y que cumpla los criterios de longitud (no menor a 8 caracteres).
3. Debe devolver el mensaje correspondiente según el resultado de cada verificación.

### Casos de Prueba y Resultados Esperados

Dado el siguiente diccionario de datos de ejemplo:

```python
alumnos = {
    'C1': {'clave': 'password123', 'nombre': 'Renzo', 'apellido': 'Santillán'},
    'C2': {'clave': 'securePass456', 'nombre': 'Julio', 'apellido': 'Mandujano'},
    'C3': {'clave': 'password789', 'nombre': 'Joel', 'apellido': 'Campos'}
}
```

| **Caso de Prueba**                           | **Descripción**                                                                                     | **Resultado Esperado**                                                        |
|----------------------------------------------|-----------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------|
| `inicioSesion('C1', 'password123')`          | Alumno con código "C1" (Renzo Santillán) y clave correcta.                                           | `"Inicio de sesión exitoso. Bienvenido Renzo Santillán"`                      |
| `inicioSesion('C2', 'wrongPass')`            | Alumno con código "C2" (Julio Mandujano) y clave incorrecta.                                         | `"Clave incorrecta"`                                                          |
| `inicioSesion('C3', 'pass')`                 | Alumno con código "C3" (Joel Campos) y clave incorrecta o de menos de 8 caracteres.                  | `"Clave incorrecta"`                                                          |
| `inicioSesion('C4', 'anyPassword')`          | Alumno con código "C4" no existe en el sistema.                                                     | `"Usuario no encontrado"`                                                     |
| `inicioSesion('C1', 'password')`             | Alumno con código "C1" (Renzo Santillán) con clave incorrecta o de 8 caracteres, pero incorrecta.    | `"Clave incorrecta"`                                                          |

---
## Listar cursos
---
### Descripción General

Desarrollar una función en Python que permita listar los cursos en los que está inscrito un alumno específico, con la capacidad de filtrar los cursos por su estado (`aprobado` o `desaprobado`) y ordenar los resultados de mayor a menor nota.

### Detalle de la Funcionalidad

- **Función:** `listarCursosPorAlumno(codigo, estado, ordenarPorNota)`
  
  - **Parámetros:**
    - `codigo` (str): Código único del alumno.
    - `estado` (str): Estado del curso a filtrar. Puede ser "aprobado", "desaprobado" o "todos".
    - `ordenarPorNota` (bool): Determina si los cursos se ordenan de mayor a menor nota (`True` para mayor y `False` para menor).

  - **Salida:**
    Una lista de diccionarios que contiene la información de los cursos:
    - `id` (str): Identificador único del curso.
    - `nombreCurso` (str): Nombre del curso.
    - `nota` (float): Nota obtenida en el curso.
    - `grado` (str): Grado en el que se imparte el curso.
    - `profesor` (str): Nombre del profesor que imparte el curso.
    - `estado` (str): Estado de aprobación del curso ("aprobado", "desaprobado" y "todos").

### Criterios de Aceptación

1. La función debe devolver una lista de cursos filtrados correctamente por el estado solicitado.
2. Los cursos deben ordenarse de mayor a menor nota si el parámetro `ordenarPorNota` es `True`.
3. La lista devuelta debe contener los campos especificados (`id`, `nombreCurso`, `nota`, `grado`, `profesor`, `estado`).
4. Si no hay cursos que coincidan con los criterios de búsqueda, la función debe devolver una lista vacía.

### Casos de Prueba y Resultados Esperados

Dado el siguiente diccionario de datos de ejemplo:

```python
"C1" : [
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
## Listado de Pagos
---
Desarrollar una función en Python que permita listar los pagos realizados por un alumno, con la capacidad de filtrar por estado (`Pagado`, `Pendiente`, `Vencido`, `Todos`) y por fecha (a partir de una fecha específica).

### Detalle de la Funcionalidad

- **Función:** `listarPagosPorAlumno(codigo, estado, desde)`
  
  - **Parámetros:**
    - `codigo` (str): Código único del alumno.
    - `estado` (str): Estado del pago a filtrar. Puede ser "Pagado", "Pendiente", "Vencido" o "todos".
    - `desde` (str, formato `YYYY-MM-DD`): Filtrar los pagos realizados a partir de esta fecha.

  - **Salida:**
    Una lista de diccionarios con la información de los pagos:
    - `codigoPago` (str): Identificador único del pago.
    - `fecha` (str, formato `YYYY-MM-DD`): Fecha del pago.
    - `monto` (float): Monto del pago.
    - `estado` (str): Estado del pago ("Pagado", "Pendiente", "Vencido").

### Criterios de Aceptación

1. La función debe devolver una lista de pagos filtrados correctamente por el estado solicitado.
2. Si se proporciona una fecha, la función solo debe mostrar los pagos realizados desde esa fecha en adelante.
3. Si no hay pagos que coincidan con los criterios de búsqueda, la función debe devolver una lista vacía.

### Casos de Prueba y Resultados Esperados

Dado el siguiente diccionario de ejemplo:

```python
pagos = {
    'C1': [
        {'codigoPago': 'P101', 'fecha': '2024-01-15', 'monto': 200.0, 'estado': 'Pagado'},
        {'codigoPago': 'P102', 'fecha': '2024-02-10', 'monto': 150.0, 'estado': 'Pendiente'},
        {'codigoPago': 'P103', 'fecha': '2024-03-05', 'monto': 300.0, 'estado': 'Vencido'}
    ]
}
```

| **Caso de Prueba**                                          | **Descripción**                                                                 | **Resultado Esperado**                                                                                                  |
|-------------------------------------------------------------|---------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------|
| `listarPagosPorAlumno('C1', 'Pagado', '2024-01-01')`        | Filtra los pagos "Pagado" a partir del 1 de enero de 2024.                       | `[{'codigoPago': 'P101', 'fecha': '2024-01-15', 'monto': 200.0, 'estado': 'Pagado'}]`                                       |
| `listarPagosPorAlumno('C1', 'Pendiente', '2024-02-01')`     | Filtra los pagos "Pendiente" a partir del 1 de febrero de 2024.                  | `[{'codigoPago': 'P102', 'fecha': '2024-02-10', 'monto': 150.0, 'estado': 'Pendiente'}]`                                    |
| `listarPagosPorAlumno('C1', 'todos', '2024-01-01')`         | Muestra todos los pagos a partir del 1 de enero de 2024.                         | `[{'codigoPago': 'P101', 'fecha': '2024-01-15', 'monto': 200.0, 'estado': 'Pagado'}, {'id': 'P102', 'fecha': '2024-02-10', 'monto': 150.0, 'estado': 'Pendiente'}, {'codigoPago': 'P103', 'fecha': '2024-03-05', 'monto': 300.0, 'estado': 'Vencido'}]` |

---
## Obtener descuento
---
### Descripción General

Desarrollar una función en Python que calcule el descuento para un pago basado en el concepto del pago (por ejemplo, matrícula, pensión, cuota de ingreso) y la categoría del alumno.

### Tabla de Descuentos

| **Categoría**   | **Concepto**     | **Descuento** |
|-----------------|------------------|---------------|
| ELIM            | Matrícula        | 5%            |
| ELIM            | Pensión          | 0%            |
| ELIM            | Cuota Ingreso    | 7%            |
| Internacional   | Matrícula        | 100%          |
| Internacional   | Pensión          | 9%            |
| Internacional   | Cuota Ingreso    | 50%           |

### Detalle de la Funcionalidad

- **Función:** `calcularDescuento(concepto, categoria, monto)`
  
  - **Parámetros:**
    - `concepto` (str): El concepto del pago (por ejemplo, "Pension", "cuotaIngreso", "Matricula").
    - `categoria` (str): Categoría del alumno (por ejemplo, "ELIM", "Internacional").
    - `monto` (float): El monto total del pago antes del descuento.

  - **Salida:**
    - Un diccionario con los siguientes campos:
      - `descuento` (str): El porcentaje de descuento en formato cadena (por ejemplo, `"20%"`).
      - `montoDescuento` (float): El monto descontado, calculado según el porcentaje de descuento.
      - `montoFinal` (float): El monto total a pagar después del descuento.

### Criterios de Aceptación

1. La función debe devolver el porcentaje de descuento correcto según el concepto y la categoría del alumno.
2. El monto final debe reflejar correctamente el descuento aplicado.
3. Si el concepto o categoría no están definidos en la tabla, no se aplicará ningún descuento.

### Casos de Prueba y Resultados Esperados

| **Caso de Prueba**                                       | **Descripción**                                                                     | **Resultado Esperado**                                                                                          |
|----------------------------------------------------------|-------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|
| `calcularDescuento('Matricula', 'ELIM', 1000.0)`         | Calcula el descuento para un alumno de categoría "ELIM" con el concepto "Matricula". | `{'descuento': '5%', 'montoDescuento': 50.0, 'montoFinal': 950.0}`                                             |
| `calcularDescuento('Pension', 'Internacional', 1000.0)`  | Calcula el descuento para un alumno de categoría "Internacional" con el concepto "Pension". | `{'descuento': '9%', 'montoDescuento': 90.0, 'montoFinal': 910.0}`                                              |
| `calcularDescuento('cuotaIngreso', 'Internacional', 2000.0)` | Calcula el descuento para un alumno de categoría "Internacional" con el concepto "cuotaIngreso". | `{'descuento': '50%', 'montoDescuento': 1000.0, 'montoFinal': 1000.0}`                                        |
| `calcularDescuento('Pension', 'ELIM', 1000.0)`           | Calcula el descuento para un alumno de categoría "ELIM" con el concepto "Pension".   | `{'descuento': '0%', 'montoDescuento': 0.0, 'montoFinal': 1000.0}`                                              |

---
## A cerca de
---
Este proyecto es parte del curso **Introducción a la Programación con Python (IAP)** ofrecido por **Kodytec**.  
Para más información sobre el curso y otros proyectos, visita nuestro sitio web https://kodytec.pe o contáctanos directamente al +51 968491916.  
**Kodytec** se compromete a brindar educación de calidad en el campo de la programación y tecnología a colegios nacionales y particulares.

---
