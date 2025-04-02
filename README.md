# Prueba Técnica - PHP y JavaScript

## Objetivo

Desarrollar un sistema de gestión de productos y ventas utilizando PHP para el backend y JavaScript para la consulta y actualización de datos en el frontend.

## Requisitos

- PHP (Backend para CRUD y lógica de negocio)
- MySQL (Base de datos)
- JavaScript (Consultas y actualización de la UI mediante AJAX o Fetch API)
- HTML + CSS (Interfaz básica con Bootstrap opcional)

---

## 1️⃣ Base de Datos

### **Estructura de Tablas**

```sql
CREATE DATABASE prueba_tecnica;
USE prueba_tecnica;

CREATE TABLE productos (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(100),
    precio DECIMAL(10,2),
    stock INT,
    estatus ENUM('disponible', 'agotado') DEFAULT 'disponible'
);

CREATE TABLE ventas (
    id INT AUTO_INCREMENT PRIMARY KEY,
    fecha TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    total DECIMAL(10,2)
);

CREATE TABLE detalle_ventas (
    id INT AUTO_INCREMENT PRIMARY KEY,
    venta_id INT,
    producto_id INT,
    cantidad INT,
    subtotal DECIMAL(10,2),
    FOREIGN KEY (venta_id) REFERENCES ventas(id) ON DELETE CASCADE,
    FOREIGN KEY (producto_id) REFERENCES productos(id) ON DELETE CASCADE
);
```

### **Datos de Prueba**

```sql
INSERT INTO productos (nombre, precio, stock, estatus) VALUES
('Laptop HP', 12000.50, 10, 'disponible'),
('Mouse Logitech', 350.75, 5, 'disponible'),
('Teclado Mecánico', 850.00, 0, 'agotado'),
('Monitor Samsung', 4500.99, 15, 'disponible'),
('Impresora Epson', 3200.00, 2, 'disponible');
```

---

## 2️⃣ Funcionalidades

### **A) CRUD de Productos (PHP)**

✅ Agregar, editar y eliminar productos desde PHP.  
✅ El estatus cambia automáticamente a `agotado` si el stock es 0.  
✅ Si el stock se actualiza a >0, cambia a `disponible`.

### **B) Registrar Ventas (PHP + JS)**

✅ Formulario donde el usuario seleccione productos y cantidad.  
✅ Calcular el total antes de confirmar la venta.  
✅ Al registrar la venta:

- Restar la cantidad vendida del stock.
- Si un producto queda en 0, cambiar su estatus a `agotado`.
- Guardar los productos vendidos en la tabla `detalle_ventas`.
- Actualizar el total de la venta en la tabla `ventas`.

### **C) Historial de Ventas (JS + PHP)**

✅ Mostrar una lista de ventas registradas.  
✅ Consultar detalles de cada venta usando JavaScript (AJAX o Fetch).  
✅ Mostrar los productos vendidos dentro de cada venta.  

---

## 3️⃣ Entregables

🔹 **Backend en PHP** con CRUD de productos y ventas.  
🔹 **Frontend en HTML, CSS y JavaScript** con consultas dinámicas.  
🔹 **Script SQL** con las tablas y datos de prueba.  

---

## 4️⃣ Criterios de Evaluación

✅ Correcta implementación de PHP y MySQL.  
✅ Uso de JavaScript para cargar datos dinámicamente.  
✅ Validaciones de stock y estatus en PHP.  
✅ Código estructurado y limpio.  

---

💡 **Extras Opcionales (Para Mejor Puntuación)**
🚀 Usar Fetch API para actualizar datos sin recargar la página.  
🚀 Implementar SweetAlert para mensajes de confirmación.  
🚀 Agregar Bootstrap para mejorar el diseño.  

🎯 **Entrega final:** Url del repositorio en github