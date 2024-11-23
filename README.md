# SQL_coder
Descripción de la Temática
Temática: Sistema de Gestión de Equipos de Fútbol
La base de datos está diseñada para gestionar la información relacionada con equipos de fútbol, incluyendo jugadores, entrenadores, partidos y transferencias. Su objetivo es proporcionar una estructura organizada para almacenar y consultar datos relevantes, facilitar la gestión de los equipos y el seguimiento de los resultados de los partidos.
Diagramas de Entidad-Relación
Entidades: Jugador, Equipo, Partido, Entrenador, Transferencia
Relaciones:
Un equipo tiene muchos jugadores.
Un Entrenador dirige un equipo.
Un partido es jugado entre dos equipos.
Una Transferencia de un Jugador entre dos Equipos.




Listado de las Tablas que Componen la Base
Tabla: Jugador
Descripción: Almacena información de los jugadores.
Campos:
id: INT, Clave primaria
nombre: VARCHAR(50)
apellido: VARCHAR(50)
posición: VARCHAR(30)
fecha_nacimiento: DATE
nacionalidad: VARCHAR(50)
Tabla: Equipo
Descripción: Almacena información de los equipos.
Campos:
id: INT, Clave primaria
nombre: VARCHAR(50)
fundacion: DATE
estadio: VARCHAR(50)
Tabla: Partido
Descripción: Almacena información de los partidos jugados.
Campos:
id: INT, Clave primaria
equipo_local_id: INT, Clave foránea
equipo_visitante_id: INT, Clave foránea
fecha: DATE
estadio: VARCHAR(50)
goles_local: INT
goles_visitante: INT
Tabla: Entrenador
Descripción: Almacena información de los entrenadores.
Campos:
id: INT, Clave primaria
nombre: VARCHAR(50)
apellido: VARCHAR(50)
equipo_id: INT, Clave foránea

Tabla: Transferencia
Descripción: Almacena información de las transferencias de jugadores.
Campos:
id: INT, Clave primaria
jugador_id: INT, Clave foránea
equipo_origen_id: INT, Clave foránea
equipo_destino_id: INT, Clave foránea
fecha_transferencia: DATE
monto: DECIMAL(10, 2)
 Archivo .sql
Script sql
CREATE DATABASE gestion_equipos_futbol;

USE gestion_futbol;

CREATE TABLE Jugador (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(50),
    apellido VARCHAR(50),
    posicion VARCHAR(30),
    fecha_nacimiento DATE,
    nacionalidad VARCHAR(50)
);

CREATE TABLE Equipo (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(50),
    fundacion DATE,
    estadio VARCHAR(50)
);

CREATE TABLE Partido (
    id INT AUTO_INCREMENT PRIMARY KEY,
    equipo_local_id INT,
    equipo_visitante_id INT,
    fecha DATE,
    estadio VARCHAR(50),
    goles_local INT,
    goles_visitante INT,
    FOREIGN KEY (equipo_local_id) REFERENCES Equipo(id),
    FOREIGN KEY (equipo_visitante_id) REFERENCES Equipo(id)
);

CREATE TABLE Entrenador (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(50),
    apellido VARCHAR(50),
    equipo_id INT,
    FOREIGN KEY (equipo_id) REFERENCES Equipo(id)
);

CREATE TABLE Transferencia (
    id INT AUTO_INCREMENT PRIMARY KEY,
    jugador_id INT,
    equipo_origen_id INT,
    equipo_destino_id INT,
    fecha_transferencia DATE,
    monto DECIMAL(10, 2),
    FOREIGN KEY (jugador_id) REFERENCES Jugador(id),
    FOREIGN KEY (equipo_origen_id) REFERENCES Equipo(id),
    FOREIGN KEY (equipo_destino_id) REFERENCES Equipo(id)
);
