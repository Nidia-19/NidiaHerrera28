-- Crear la base de datos para practicar roles y usuarios
CREATE DATABASE Liz;

-- Seleccionar la base de datos recién creada
USE Liz;

-- Crear tabla 'Autores' con campos básicos
CREATE TABLE Autores (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nombre VARCHAR(100) NOT NULL,
    nacionalidad VARCHAR(50)
);

-- Crear tabla 'Libros' con relación a 'Autores'
CREATE TABLE Libros (
    id INT PRIMARY KEY AUTO_INCREMENT,
    titulo VARCHAR(100) NOT NULL,
    autor_id INT,
    anio_publicacion INT,
    FOREIGN KEY (autor_id) REFERENCES Autores(id)
);

-- Crear tabla 'Usuarios' del sistema
CREATE TABLE Usuarios (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nombre VARCHAR(100) NOT NULL,
    correo VARCHAR(100) UNIQUE NOT NULL
);

-- Crear roles que simulan distintos tipos de usuarios del sistema
CREATE ROLE lectora;
CREATE ROLE editor;
CREATE ROLE admin_libros;

-- Asignar permisos al rol 'lectora': solo puede leer los libros
GRANT SELECT ON Liz.Libros TO 'lectora';

-- Asignar permisos al rol 'editor': puede leer, insertar y actualizar libros; leer autores
GRANT SELECT, INSERT, UPDATE ON Liz.Libros TO 'editor';
GRANT SELECT ON Liz.Autores TO 'editor';

-- Asignar permisos al rol 'admin_libros': acceso total a todas las tablas
GRANT SELECT, INSERT, UPDATE, DELETE ON Liz.* TO 'admin_libros';

-- Aplicar los cambios de privilegios
FLUSH PRIVILEGES;

-- Crear usuarios con sus respectivas contraseñas
CREATE USER 'nidia'@'localhost' IDENTIFIED BY 'password';
CREATE USER 'carlos'@'localhost' IDENTIFIED BY 'password';
CREATE USER 'ana'@'localhost' IDENTIFIED BY 'password';

-- Asignar roles a los usuarios creados
GRANT 'lectora' TO 'nidia'@'localhost';
GRANT 'editor' TO 'carlos'@'localhost';
GRANT 'admin_libros' TO 'ana'@'localhost';

-- Consulta correcta para listar usuarios y sus hosts
SELECT User, Host FROM mysql.user;

-- Ver privilegios asignados al usuario nidia
SHOW GRANTS FOR 'nidia'@'localhost';

-- Ver privilegios asignados al usuario carlos
SHOW GRANTS FOR 'carlos'@'localhost';

-- Ver privilegios asignados al usuario ana
SHOW GRANTS FOR 'ana'@'localhost';

-- Ver privilegios que tiene el rol 'admin_libros'
SHOW GRANTS FOR 'admin_libros';
