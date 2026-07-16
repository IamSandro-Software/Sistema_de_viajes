# Especificación de Requisitos de Software (SRS) Ligero
## Sistema de Control de Inventario - Tienda Local

**Versión:** 1.0
**Fecha:** 2026-07-15
**Elaborado por:** [Nombre de tu Equipo]
**Cliente:** Tienda "El Buen Precio"

---

## 1. Alcance del Sistema

### 1.1. ¿Qué hará el sistema?
El sistema "Control de Inventario" permitirá a la tienda local:
*   Gestionar el catálogo de productos (altas, bajas, modificaciones y consultas).
*   Controlar las entradas y salidas de inventario (compras a proveedores y ventas a clientes).
*   Generar alertas de stock mínimo para evitar desabastecimiento.
*   Emitir informes básicos de valor de inventario y productos más vendidos.

### 1.2. ¿Qué NO hará el sistema? (Fuera de Alcance)
*   No gestionará la contabilidad general de la tienda (libros contables, impuestos).
*   No tendrá un módulo de gestión de clientes o CRM avanzado.
*   No se integrará con plataformas de comercio electrónico en esta fase.
*   No manejará envíos ni logística de distribución.

---

## 2. Perspectiva y Actores

El sistema tendrá una interfaz web accesible desde cualquier navegador moderno. Los actores o usuarios que interactuarán con él son:

*   **Administrador:** Es el dueño o gerente de la tienda. Tendrá acceso a todas las funciones del sistema: gestión de productos, usuarios (dar de alta a empleados), informes y configuración.
*   **Empleado de Tienda:** Es el personal de mostrador. Sus permisos se limitarán a:
    *   Consultar el stock de productos.
    *   Realizar ventas (que disminuyan el inventario).
    *   Registrar la recepción de mercancía (que aumente el inventario).
    *   No podrá modificar precios ni eliminar productos.

---

## 3. Requisitos Funcionales (Historias de Usuario)

A continuación, se listan los requisitos funcionales del sistema, agrupados por módulo lógico.

### 3.1. Módulo: Gestión de Productos (REQ-PROD)
*   **REQ-PROD-001:** *Como Administrador, quiero poder agregar un nuevo producto al inventario, especificando su nombre, descripción, precio, categoría y stock inicial.*
*   **REQ-PROD-002:** *Como Administrador, quiero poder modificar la información de un producto existente (ej. precio, nombre, categoría).*
*   **REQ-PROD-003:** *Como Empleado, quiero poder buscar un producto por su nombre o código de barras para consultar su stock y precio.*
*   **REQ-PROD-004:** *Como Administrador, quiero poder dar de baja (desactivar) un producto que ya no se venda, sin eliminarlo de la base de datos para mantener el historial.*

### 3.2. Módulo: Gestión de Inventario (REQ-INV)
*   **REQ-INV-001:** *Como Empleado, quiero registrar la entrada de mercancía de un proveedor, incrementando el stock de los productos correspondientes.*
*   **REQ-INV-002:** *Como Empleado, quiero registrar una venta, lo que debe decrementar automáticamente el stock de los productos vendidos.*
*   **REQ-INV-003:** *Como Administrador, quiero que el sistema muestre una alerta (visual y/o por correo) cuando el stock de un producto caiga por debajo de un nivel mínimo predefinido.*
*   **REQ-INV-004:** *Como Administrador, quiero poder ajustar el stock de un producto manualmente en caso de mermas o errores de conteo (inventario físico).*

### 3.3. Módulo: Reportes (REQ-REP)
*   **REQ-REP-001:** *Como Administrador, quiero generar un informe del valor total del inventario en un momento dado.*
*   **REQ-REP-002:** *Como Administrador, quiero generar un informe de los productos más vendidos en un período de tiempo seleccionado.*

---

## 4. Restricciones Tecnológicas

El sistema deberá desarrollarse bajo las siguientes condiciones:

*   **Lenguaje de Programación:** Python (versión 3.10 o superior) usando el framework Django.
*   **Base de Datos:** PostgreSQL (versión 14 o superior).
*   **Frontend:** HTML5, CSS3 y JavaScript (con Bootstrap 5 para el diseño).
*   **Control de Versiones:** Git y GitHub (código fuente y documentación).
*   **Navegadores Compatibles:** Las dos últimas versiones de Google Chrome, Mozilla Firefox y Microsoft Edge.
*   **Entorno de Despliegue:** El sistema debe ser desplegable en un servidor Linux (Ubuntu 22.04 LTS) usando Docker o un PaaS como Heroku o Railway.

---

## 5. Matriz de Trazabilidad de Requisitos

Esta matriz asegura que cada requisito funcional tiene una correspondencia directa con las fases de diseño, desarrollo y pruebas del proyecto.

| ID del Requisito | Fuente (Historia de Usuario) | Componente de Diseño | Módulo de Código | Caso de Prueba | Estado |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **REQ-PROD-001** | 3.1. Gestión de Productos | - | - | - | Pendiente |
| **REQ-PROD-002** | 3.1. Gestión de Productos | - | - | - | Pendiente |
| **REQ-PROD-003** | 3.1. Gestión de Productos | - | - | - | Pendiente |
| **REQ-PROD-004** | 3.1. Gestión de Productos | - | - | - | Pendiente |
| **REQ-INV-001** | 3.2. Gestión de Inventario | - | - | - | Pendiente |
| **REQ-INV-002** | 3.2. Gestión de Inventario | - | - | - | Pendiente |
| **REQ-INV-003** | 3.2. Gestión de Inventario | - | - | - | Pendiente |
| **REQ-INV-004** | 3.2. Gestión de Inventario | - | - | - | Pendiente |
| **REQ-REP-001** | 3.3. Reportes | - | - | - | Pendiente |
| **REQ-REP-002** | 3.3. Reportes | - | - | - | Pendiente |