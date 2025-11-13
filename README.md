# 📘 Sistema de Gestión de Biblioteca

## Caso de Uso: CU-01 — Préstamo de Libros

### Resumen  
Permite a un usuario registrado solicitar el préstamo de un libro, registrar la operación y controlar devoluciones y sanciones.

---

## Diagrama de Caso de Uso (UML)  
```mermaid
usecaseDiagram
    actor Usuario as U
    actor Bibliotecario as B
    actor "Sistema Externo\n(Autenticación)" as SE

    rectangle "Sistema Biblioteca" {
        usecase "Buscar libro" as UC_Buscar
        usecase "Ver disponibilidad" as UC_VerDisponibilidad
        usecase "Solicitar préstamo" as UC_Solicitar
        usecase "Registrar préstamo" as UC_Registrar
        usecase "Reservar libro" as UC_Reservar
        usecase "Devolver libro" as UC_Devolver
        usecase "Registrar devolución" as UC_RegistrarDevol
        usecase "Consultar préstamos activos" as UC_Consultar
    }

    U --> UC_Buscar
    U --> UC_VerDisponibilidad
    U --> UC_Solicitar
    U --> UC_Reservar
    U --> UC_Devolver
    U --> UC_Consultar

    B --> UC_Registrar
    B --> UC_RegistrarDevol
    SE --> UC_Solicitar
    SE --> UC_Registrar

    UC_Solicitar --> UC_VerDisponibilidad : <<include>>
    UC_Solicitar --> UC_Registrar : <<include>>
    UC_Devolver --> UC_RegistrarDevol : <<include>>
    UC_Buscar ..> UC_VerDisponibilidad : <<extend>>
