### CREACIÓN DE DATABASE

------

```sql
DROP DATABASE IF EXISTS SENA_PROYECTO;
CREATE DATABASE SENA_PROYECTO;
USE SENA_PROYECTO;
```
### ELIMINAR TABLAS ANTERIORES  DE DATABASE

------

```
DROP TABLE IF EXISTS Carrera;
DROP TABLE IF EXISTS Cursos;
DROP TABLE IF EXISTS Estudiante;
DROP TABLE IF EXISTS Rutas;
DROP TABLE IF EXISTS Instructor;
DROP TABLE IF EXISTS Matricula;
DROP TABLE IF EXISTS Cursos_Ruta;
DROP TABLE IF EXISTS Clase_estudiante;
```

### CREACIÓN DE TABLAS

------

```sql
CREATE TABLE curso (
    id_curso int NOT NULL PRIMARY KEY,
    curso varchar(32) NOT NULL
    );

CREATE TABLE carrera (
    id_carrera INT NOT NULL PRIMARY KEY,
    carrera VARCHAR(255) NOT NULL
);

CREATE TABLE estudiante (
    id_estudiante int NOT NULL,
    nombre varchar(32) NOT NULL,
    apellido varchar(32) NOT NULL,
    edad int NOT NULL,
    PRIMARY KEY (id_estudiante)
    );

CREATE TABLE rutas (
    id_ruta int NOT NULL,
    ruta varchar(50) DEFAULT NULL,
    id_carrera int NOT NULL,
    PRIMARY KEY (id_ruta),
    FOREIGN KEY (id_carrera) REFERENCES Carrera (id_carrera)
    );

CREATE TABLE instructor (
    id_instructor int NOT NULL,
    instructor varchar(32) NOT NULL,
    especialidad varchar(32) NOT NULL,
    PRIMARY KEY (id_instructor)
    );

CREATE TABLE matricula (
    id_estudiante int NOT NULL,
    id_ruta int NOT NULL,
    estado ENUM('En Ejecución', 'Terminado', 'Cancelado'),
    FOREIGN KEY (id_estudiante) REFERENCES estudiante (id_estudiante),
    FOREIGN KEY (id_ruta) REFERENCES Rutas (id_ruta),
    CONSTRAINT MatriculaxAprendiz UNIQUE (id_estudiante, id_ruta, estado)
);

CREATE TABLE Cursos_Ruta (
    id_clase int NOT NULL AUTO_INCREMENT,
    id_ruta int NOT NULL,
    id_curso int NOT NULL,
    id_instructor int NULL,
    CONSTRAINT CursoxRuta UNIQUE (id_ruta, id_curso, id_instructor),
    PRIMARY KEY (id_clase)
);

CREATE TABLE Clase_estudiante (
    id_estudiante int NOT NULL,
    id_clase int NOT NULL,
    FOREIGN KEY (id_estudiante) REFERENCES estudiante (id_estudiante),
    FOREIGN KEY (id_clase) REFERENCES Cursos_Ruta (id_clase),
    PRIMARY KEY (id_estudiante, id_clase)
);
```

### INFORMACIÓN PARA POBLAR

------

```sql
INSERT INTO curso (id_curso, curso)
VALUES 
(1,'Matemáticas Básicas'),
(2,'Álgebra Computacional'),
(3,'Programación Básica'),
(4,'Inglés'),
(5,'Electrónica Básica'),
(6,'Motor de Cuatro Tiempos'),
(7,'Enfermedades Laborales'),
(8,'Higiene Postural en el Trabajo'),
(9,'Ergonomía'),
(10,'Legislación Laboral en Colombia'),
(11,'Materiales de Soldadura'),
(12,'Métodos de Soldadura'),
(13,'Fusión de Metales'),
(14,'Buceo 1'),
(15,'Buceo 2'),
(16,'Riesgo Eléctrico'),
(17,'Bases de Datos Relacionales'),
(18,'Bases de Datos NO Relacionales'),
(19,'Electrónica Digital'),
(20,'Microprocesadores');

INSERT INTO carrera (id_carrera, carrera)
VALUES 
(1,'Desarrollo de Software'), 
(2,'Electrónica'), 
(3,'Mecánica Automotriz'), 
(4,'Seguridad y Salud Ocupacional'), 
(5,'Soldadura');


INSERT INTO estudiante  (id_estudiante, nombre, apellido, edad)
VALUES 
(1, 'Carlos Saúl', 'Gómez', 17), 
(2, 'Leyla María', 'Delgado Vargas', 18), 
(3, 'Juan José', 'Martinez', 19), 
(4, 'Sergio Augusto' , 'Contreras Navas', 20), 
(5, 'Ana María', 'Velasquez Parra', 17), 
(6, 'Gustavo', 'Noriega Alzate', 18), 
(7, 'Pedro Nell', 'Gómez Díaz', 19), 
(8, 'Jairo Augusto', 'Castro Camargo', 20), 
(9, 'Henry', 'Soler Vega', 17), 
(10, 'Antonio', 'Cañate Cortés', 18), 
(11, 'Daniel', 'Simancas Junior', 19);


INSERT INTO rutas (id_ruta,ruta,id_carrera)
VALUES 
(1,'Sistemas de Información Empresariales',1),
(2,'Videojuegos',1),
(3,'Machine Learning',1),
(4,'Microcontroladores',2),
(5,'Robótica',2),
(6,'Dispositivos Bio-médicos',2),
(7,'Motores Híbridos',3),
(8,'Vehículos de Uso Agrícola',3),
(9,'Sistemas de Gestión en Seguridad Ocupacional',4),
(10,'Soldadura Autógena Industrial',5),
(11,'Soldadura Eléctrica Industrial',5),
(12,'Soldadura Submarina',5);

INSERT INTO Instructor (id_instructor, instructor, especialidad)
VALUES 
(1, 'Ricardo Vicente Jaimes', 'Sistemas'), 
(2, 'Marinela Narvaez', 'Salud Ocupacional'), 
(3, 'Agustín Parra Granados', 'Soldadura'), 
(4, 'Nelson Raúl Buitrago', 'Mecánica'), 
(5, 'Roy Hernando Llamas', 'Inglés'), 
(6, 'Maria Jimena Monsalve', 'Electrónica'), 
(7, 'Juan Carlos Cobos', 'Electrónica'), 
(8, 'Pedro Nell Santoamaría', 'Sistemas'), 
(9, 'Andrea González', 'Sistemas'), 
(10, 'Marisela Sevilla', 'Salud Ocupacional');

INSERT INTO matricula 
VALUES 
(1,1,1),
(2,1,1),
(3,2,3),
(4,2,1),
(5,3,1),
(6,4,2),
(7,4,2),
(8,5,2),
(9,5,3),
(10,11,2),
(11,10,2);

INSERT INTO Cursos_Ruta(id_ruta, id_curso, id_instructor) 
VALUES 
(1,17,2), 
(1,2,1), 
(1,18,2), 
(1,1,4), 
(1,3,3), 
(1,4,5), 
(2,1,4), 
(2,2,1), 
(2,3,3), 
(2,4,5), 
(3,3,3), 
(3,4,5), 
(3,17,2), 
(4,5,7), 
(4,19,6), 
(4,20,7), 
(5,5,7), 
(5,19,6), 
(5,20,7), 
(11,11,3), 
(11,13,3), 
(10,12,3), 
(10,14,NULL);

INSERT INTO clase_estudiante 
VALUES 
(1,1), 
(1,2), 
(1,5), 
(1,3), 
(2,4), 
(2,2), 
(2,5), 
(2,6), 
(3,7), 
(3,8), 
(3,9), 
(4,10), 
(4,7), 
(4,8), 
(5,11), 
(5,12), 
(5,13), 
(6,14), 
(6,15), 
(6,16), 
(7,14), 
(7,15), 
(7,16), 
(8,17), 
(8,18), 
(9,17), 
(9,18), 
(9,19), 
(10,20), 
(10,21), 
(11,22), 
(11,23);
```

------

### CONSULTAS PROPUESTAS

1. Agregue un campo Estado_Matrícula a la tabla Matrícula que indique si el estudiante se encuentra “En Ejecución”, “Terminado” o “Cancelado”.

   ```sql
   ADD Estado_Matricula ENUM('En Ejecución', 'Terminado', 'Cancelado');
   ```

   

2. Agregue a el campo edad a la tabla de Aprendices.

   ```sql
   ALTER TABLE estudiante
   ADD edad int NOT NULL;
   ```

3. Si suponemos que los cursos tienen una duración diferente dependiendo de la ruta que lo contenga ¿qué modificación haría a la estructura de datos ya planteada?

   ```sql
   ALTER TABLE Cursos_Ruta 
   ADD duracion int NULL DEFAULT 8;
   ```

4. Seleccionar los nombres y edades de aprendices que están cursando la carrera de electrónica.

   ```sql
   SELECT E.nombre, E.apellido, E.edad  
   FROM estudiante E 
   INNER JOIN Matricula M 
   ON E.id_estudiante=M.id_estudiante 
   WHERE M.id_ruta IN (SELECT id_ruta FROM Rutas WHERE id_carrera=2);
   ```

5. Seleccionar Nombres de Aprendices junto al nombre de la ruta de aprendizaje que cancelaron.

   ```sql
   SELECT E.nombre, E.apellido, E.edad, R.ruta FROM estudiante E 
   JOIN Matricula M ON M.id_estudiante=E.id_estudiante 
   JOIN Rutas R ON M.id_ruta=R.id_ruta WHERE M.estado='Cancelado';
   ```

6. Seleccionar Nombre de los cursos que no tienen un instructor asignado.

   ```sql
   SELECT R.ruta,C.curso 
   FROM Curso C 
   INNER JOIN Cursos_Ruta CR ON C.id_curso=CR.id_curso 
   INNER JOIN Rutas R on R.id_ruta=CR.id_ruta 
   WHERE CR.id_instructor IS NULL;
   ```

7. Seleccionar Nombres de los instructores que dictan cursos en la ruta de aprendizaje “Sistemas de Información Empresariales”.

   ```sql
   SELECT DISTINCT I.instructor AS "Instructor Sistemas de Información Empresariales" 
   FROM Instructor I 
   INNER JOIN Cursos_Ruta CR ON I.id_instructor = CR.id_instructor 
   INNER JOIN Rutas R ON R.id_ruta=CR.id_ruta 
   WHERE R.ruta='Sistemas de Información Empresariales';
   ```

8. Genere un listado de todos los aprendices que terminaron una Carrera mostrando el nombre del profesional, el nombre de la carrera y el énfasis de la carrera (Nombre de la Ruta de aprendizaje).

   ```sql
   SELECT CONCAT(E.nombre, ' ', E.apellido) AS Profesional
   FROM estudiante E 
   INNER JOIN matricula M on E.id_estudiante = M.id_estudiante
   WHERE M.estado='Terminado';
   ```

9. Genere un listado de los aprendices matriculados en el curso “Bases de Datos Relacionales”.

   ```sql
   SELECT CONCAT(E.nombre, ' ', E.apellido) AS Estudiante 
   FROM estudiante E 
   INNER JOIN clase_estudiante CE ON E.id_estudiante=CE.id_estudiante 
   INNER JOIN Cursos_Ruta CR ON CE.id_clase=CR.id_clase 
   INNER JOIN Curso C ON CR.id_curso=C.id_curso 
   WHERE C.curso='Bases de Datos Relacionales';
   ```

10. Nombres de Instructores que no tienen curso asignado.

    ```sql
    SELECT I.instructor AS "Instructores sin cursos"
    FROM Instructor I 
    LEFT JOIN Cursos_Ruta CR ON I.id_instructor=CR.id_instructor 
    WHERE CR.id_instructor IS NULL;
    ```

------

#### **¿En qué consiste filtrar con SQL?**

(A) Seleccionar datos que cumplen una condición determinada.

(B) Modificar una tabla para que cumpla una condición.

(C) Eliminar datos innecesarios de la base de datos.

(D) Eliminar registros no válidos.

*Respuesta (A)



#### **¿Qué filtro permite obtener todos los registros con valores en la columna date (fecha) entre '01-01-2024' (1º de enero de 2024) y '01-04-2024' (1º de abril de 2024)?**

(A) WHERE date BETWEEN '01-01-2024', '01-04-2024';

(B) WHERE date BETWEEN '01-01-2024' AND '01-04-2024';

(C) WHERE date < '01-04-2024';

(D) WHERE date > '01-01-2024';

*Respuesta (B)



#### **¿Cuál de las siguientes opciones describe la función de la cláusula DISTINCT en MySQL?**

(A) Devuelve todos los registros de una tabla, incluso si hay registros duplicados.

(B) Devuelve solo los registros únicos de una tabla, eliminando los registros duplicados.

(C) Devuelve solo los registros que cumplen con una condición específica, incluso si hay registros duplicados.

(D) Devuelve solo los registros que no cumplen con una condición específica, incluso si hay registros duplicados.

*Respuesta (B)



#### **¿Cuál de las siguientes opciones es la diferencia entre los comandos TRUNCATE y DROP en MySQL?**

(A) TRUNCATE elimina la tabla, mientras que DROP elimina los datos de la tabla.

(B) TRUNCATE elimina la tabla, mientras que DROP elimina la tabla y sus índices.

(C) TRUNCATE elimina los datos de la tabla, mientras que DROP elimina la tabla y sus datos.

(D) TRUNCATE elimina los datos de la tabla, mientras que DROP elimina la tabla y sus índices.

*Respuesta (C)
