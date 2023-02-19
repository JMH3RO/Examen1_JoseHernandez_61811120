# Examen1_JoseHernandez_61811120

yml
version: '3.8'
services:
  db:
    image: mcr.microsoft.com/mssql/server:2019-latest
    environment:
      SA_PASSWORD: <strong-password>
      ACCEPT_EULA: Y
      MSSQL_PID: Developer
    ports:
      - "1433:1433"

--Crea Base de dartos Mercadito     
CREATE DATABASE Mercadito;

USE Mercadito;

CREATE TABLE Proveedores (
    ProveedorID INT PRIMARY KEY,
    Nombre VARCHAR(50),
    Tipo VARCHAR(50)
);

CREATE TABLE Productos (
    ProductoID INT PRIMARY KEY,
    Nombre VARCHAR(50),
    PrecioCompra MONEY,
    PrecioVenta MONEY,
    StockMinimo INT,
    StockActual INT,
    ProveedorID INT,
    FOREIGN KEY (ProveedorID) REFERENCES Proveedores(ProveedorID)
);

CREATE TABLE Ventas (
    VentaID INT PRIMARY KEY,
    FechaVenta DATE,
    Total MONEY
);

CREATE TABLE DetalleVentas (
    DetalleVentaID INT PRIMARY KEY,
    Cantidad INT,
    PrecioUnitario MONEY,
    Total MONEY,
    VentaID INT,
    ProductoID INT,
    FOREIGN KEY (VentaID) REFERENCES Ventas(VentaID),
    FOREIGN KEY (ProductoID) REFERENCES Productos(ProductoID)
);

--Normalizacion
CREATE TABLE clientes (
  id_cliente INT PRIMARY KEY,
  nombre_cliente VARCHAR(50),
  telefono VARCHAR(15)
);

CREATE TABLE pedidos (
  id_pedido INT PRIMARY KEY,
  fecha_pedido DATE,
  id_cliente INT,
  FOREIGN KEY (id_cliente) REFERENCES clientes(id_cliente)
);

CREATE TABLE product (
  id_producto INT PRIMARY KEY,
  nombre_producto VARCHAR(50),
  precio DECIMAL(10,2)
);

CREATE TABLE detalle_pedidos (
  id_detalle INT PRIMARY KEY,
  id_pedido INT,
  id_producto INT,
  cantidad INT,
  precio_unitario DECIMAL(10,2),
  FOREIGN KEY (id_pedido) REFERENCES pedidos(id_pedido),
  FOREIGN KEY (id_producto) REFERENCES product(id_producto)
);



--Insert datos
INSERT INTO clientes (id_cliente, nombre_cliente, telefono)
VALUES 
  (1, 'Juan Pérez', '123456789'),
  (2, 'María Gómez', '987654321'),
  (3, 'Pedro Torres', '5555555555'),
  (4, 'Ana García', '4444444444'),
  (5, 'Luisa Rodríguez', '3333333333'),
  (6, 'Jorge Hernández', '2222222222'),
  (7, 'Carla Sánchez', '1111111111'),
  (8, 'Manuel Jiménez', '7777777777'),
  (9, 'Lucía Vázquez', '6666666666'),
  (10, 'Miguel Sosa', '9999999999');

INSERT INTO pedidos (id_pedido, fecha_pedido, id_cliente)
VALUES 
  (1, '2023-02-15', 1),
  (2, '2023-02-15', 3),
  (3, '2023-02-15', 5),
  (4, '2023-02-15', 7),
  (5, '2023-02-15', 9),
  (6, '2023-02-15', 2),
  (7, '2023-02-15', 4),
  (8, '2023-02-15', 6),
  (9, '2023-02-15', 8),
  (10, '2023-02-15', 10);

INSERT INTO product (id_producto, nombre_producto, precio)
VALUES 
  (1, 'Camiseta', 10.50),
  (2, 'Pantalón', 20.00),
  (3, 'Zapatos', 30.75),
  (4, 'Bufanda', 5.99),
  (5, 'Gorra', 8.50),
  (6, 'Calcetines', 3.25),
  (7, 'Sudadera', 25.00),
  (8, 'Chaqueta', 40.00),
  (9, 'Botas', 50.00),
  (10, 'Bolsa', 15.99);

INSERT INTO detalle_pedidos (id_detalle, id_pedido, id_producto, cantidad, precio_unitario)
VALUES 
  (1, 1, 1, 2, 10.50),
  (2, 2, 2, 1, 20.00),
  (3, 3, 3, 3, 30.75),
  (4, 4, 4, 4, 5.99),
  (5, 5, 5, 2, 8.50),
  (6, 6, 6, 5, 3.25),
  (7, 7, 7, 1, 25.00),
  (8, 8, 8, 2, 40.00),
  (9, 9, 9, 1, 50.00),
  (10, 10, 10, 3, 15.99);
