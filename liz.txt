-- Crear la base de datos para practicar roles y usuarios
CREATE DATABASE test_roles;

-- Seleccionar la base de datos recién creada
USE test_roles;

-- Crear tabla 'Departamentos' con un campo 'id' autoincremental y un nombre obligatorio
CREATE TABLE Departamentos (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nombre VARCHAR(100) NOT NULL
);

-- Crear tabla 'Empleados' con relación a 'Departamentos'
CREATE TABLE Empleados (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nombre VARCHAR(100) NOT NULL,
    correo VARCHAR(100) NOT NULL,
    departamento_id INT,
    salario DECIMAL(10,2),
    FOREIGN KEY (departamento_id) REFERENCES Departamentos(id)
);

-- Crear roles que simulan distintos tipos de usuarios del sistema
CREATE ROLE gerente;
CREATE ROLE recepcion;
CREATE ROLE limpieza;

-- Asignar permisos al rol 'gerente': acceso total a todas las tablas
GRANT SELECT, INSERT, DELETE, UPDATE ON test_roles.* TO 'gerente';

-- Asignar permisos al rol 'recepcion': puede leer, insertar y actualizar datos
GRANT SELECT, INSERT, UPDATE ON test_roles.* TO 'recepcion';

-- Asignar permisos al rol 'limpieza': puede leer y actualizar (por ejemplo, marcar limpieza completada)
GRANT SELECT, UPDATE ON test_roles.* TO 'limpieza';

-- Aplicar los cambios de privilegios (opcional en MySQL 8+, útil en versiones anteriores)
FLUSH PRIVILEGES;

-- Crear usuarios con sus respectivas contraseñas
CREATE USER 'Juan_Carlos'@'localhost' IDENTIFIED BY 'password';
CREATE USER 'Carlos'@'localhost' IDENTIFIED BY 'password';
CREATE USER 'Charly'@'localhost' IDENTIFIED BY 'password';

-- Asignar roles a los usuarios creados
GRANT 'gerente' TO 'Juan_Carlos'@'localhost';
GRANT 'recepcion' TO 'Carlos'@'localhost';
GRANT 'limpieza' TO 'Charly'@'localhost';

-- Mostrar usuarios creados en la base de datos (primero con error, luego corregido)
-- Esta línea contiene un error: 'localhost' no es una columna válida
-- SELECT User, localhost FROM mysql.user;

-- Consulta correcta para listar usuarios y sus hosts
SELECT User, Host FROM mysql.user;

-- Ver privilegios asignados al usuario Carlos
SHOW GRANTS FOR 'Carlos'@'localhost';

-- Ver privilegios asignados al usuario Juan_Carlos
SHOW GRANTS FOR 'Juan_Carlos'@'localhost';

-- Ver privilegios que tiene el rol 'gerente'
SHOW GRANTS FOR 'gerente';