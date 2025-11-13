# 📘 Sistema de Gestión de Biblioteca

## 🧩 Caso de Uso: Préstamo de Libros

---

### 🔖 Identificador
CU-01

### 📝 Nombre
Gestión de Préstamos de Libros

### 👤 Actor Principal
Usuario registrado (Lector)

### 👥 Actores Secundarios
- Bibliotecario  
- Sistema de Biblioteca

---

## 🧠 Descripción General
Este caso de uso permite a un usuario solicitar el préstamo de un libro disponible en la biblioteca.  
El sistema valida la disponibilidad del ejemplar, registra la información del préstamo y actualiza el estado del libro.

---

## ⚙️ Precondiciones
- El usuario debe estar registrado en el sistema.  
- El usuario no debe tener sanciones ni préstamos vencidos.  
- El libro solicitado debe estar disponible en inventario.  

---

## 🔄 Flujo Principal

| Paso | Acción del Actor | Respuesta del Sistema |
|------|------------------|------------------------|
| 1 | El usuario inicia sesión en el sistema. | Verifica credenciales y permite el acceso. |
| 2 | El usuario busca un libro por título, autor o código. | Muestra resultados de búsqueda. |
| 3 | El usuario selecciona el libro deseado. | Muestra la información detallada del libro y su disponibilidad. |
| 4 | El usuario selecciona la opción **“Solicitar préstamo”**. | Verifica disponibilidad del libro. |
| 5 | El sistema registra el préstamo con fecha actual y calcula la fecha de devolución. | Guarda el registro en la base de datos. |
| 6 | El sistema actualiza el estado del libro a **“Prestado”**. | Confirma la operación. |
| 7 | El sistema muestra un mensaje de confirmación con los detalles del préstamo. | — |

---

## ⚠️ Flujos Alternativos

**A1. Libro no disponible:**  
- Si el libro no está disponible, el sistema muestra un mensaje indicando que el ejemplar está prestado y ofrece la opción de **reservarlo**.

**A2. Usuario con sanciones:**  
- Si el usuario tiene sanciones o préstamos vencidos, el sistema no permite realizar nuevos préstamos y muestra un aviso con la razón.

---

## ✅ Postcondiciones
- El préstamo queda registrado correctamente en la base de datos.  
- El libro cambia su estado a **“Prestado”**.  
- El usuario puede visualizar el préstamo activo desde su cuenta.

---

## 🧾 Reglas de Negocio
1. Un usuario puede tener máximo **3 préstamos activos**.  
2. La duración estándar de un préstamo es de **7 días**.  
3. Si el libro no es devuelto a tiempo, el sistema genera una **sanción automática**.  
4. Solo los usuarios registrados pueden acceder al servicio de préstamo.

---

## 💾 Datos Involucrados
| Campo | Tipo de Dato | Descripción |
|--------|---------------|-------------|
| ID_Usuario | Entero | Identificador único del usuario. |
| ID_Libro | Entero | Identificador único del libro. |
| Fecha_Préstamo | Fecha | Fecha en la que se realiza el préstamo. |
| Fecha_Devolución | Fecha | Fecha límite para devolver el libro. |
| Estado | Texto | Indica si el libro está “Disponible”, “Prestado” o “Reservado”. |

---

## 🧩 Ejemplo de Registro en Base de Datos (SQL)
```sql
INSERT INTO prestamos (id_usuario, id_libro, fecha_prestamo, fecha_devolucion, estado)
VALUES (102, 45, '2025-11-13', '2025-11-20', 'Prestado');
