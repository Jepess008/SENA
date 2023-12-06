# Proyecto BASES DE DATOS

JEFFERSON DARIO BELTRAN LASPRILLA - Campuslands

### Creacion y poblacion de las tablas


```sql
   CREATE DATABASE SENA;
   USE SENA;

   CREATE TABLE APRENDIZ(
    ID_APRENDIZ INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    NOMBRE_APRENDIZ VARCHAR(20),
    APELLIDO_APRENDIZ VARCHAR(20)
);

CREATE TABLE MATRICULA(
    ID_MATRICULA INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    ID_RUTA INT,
    ID_APRENDIZ INT NOT NULL
);

CREATE TABLE RUTA(
    ID_RUTA INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    NOMBRE_RUTA VARCHAR (20),
    ID_CARRERA INT NOT NULL
);

CREATE TABLE CARRERA(
    ID_CARRERA INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    NOMBRE_CARRERA VARCHAR(40)
);

CREATE TABLE RUTAS_X_CURSO(
    ID_RUTA INT NOT NULL,
    ID_CURSO INT NOT NULL,
    DURACION VARCHAR(30)
);

CREATE TABLE CURSO(
    ID_CURSO INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    NOMBRE_CURSO VARCHAR(30)
);


CREATE TABLE INSTRUCTOR(
    ID_INSTRUCTOR INT NOT NULL PRIMARY KEY,
    NOMBRE_INSTRUCTOR VARCHAR (30),
    APELLIDO_INSTRUCTOR VARCHAR (30),
    ESPECIALIDAD VARCHAR(20)
);
CREATE TABLE CURSO_INSTRUCTOR(
    ID_CURSO INT,
    ID_INSTRUCTOR INT,
    FOREIGN KEY(ID_CURSO) REFERENCES CURSO(ID_CURSO),
    FOREIGN KEY(ID_INSTRUCTOR) REFERENCES INSTRUCTOR(ID_INSTRUCTOR)
);
```

### HAGO LOS ALTER NECESARIOS SEGUN MI PLANTEAMIENTO
```sql
ALTER TABLE `MATRICULA`
ADD CONSTRAINT FK_MATRICULA_APRENDIZ
FOREIGN KEY (ID_APRENDIZ)
REFERENCES `APRENDIZ`(ID_APRENDIZ);

ALTER TABLE `MATRICULA`
ADD CONSTRAINT FK_MATRICULA_RUTA
FOREIGN KEY (ID_RUTA)
REFERENCES `RUTA`(ID_RUTA);

ALTER TABLE `RUTA`
ADD CONSTRAINT FK_RUTA_CARRERA
FOREIGN KEY (ID_CARRERA)
REFERENCES `CARRERA` (ID_CARRERA);

ALTER TABLE `RUTAS_X_CURSO`
ADD CONSTRAINT FK_RUTAS_X_CURSO_RUTA
FOREIGN KEY (ID_RUTA)
REFERENCES `RUTA` (ID_RUTA);

ALTER TABLE `RUTAS_X_CURSO`
ADD CONSTRAINT FK_RUTAS_X_CURSO_CURSO
FOREIGN KEY (ID_CURSO)
REFERENCES `CURSO` (ID_CURSO);

ALTER TABLE `RUTA`
MODIFY NOMBRE_RUTA VARCHAR(50);

ALTER TABLE `CURSO`
MODIFY NOMBRE_CURSO VARCHAR(50);

ALTER TABLE `MATRICULA` ADD ID_CURSO INT

ALTER TABLE `MATRICULA`
ADD CONSTRAINT FK_MATRICULA_CURSO
FOREIGN KEY(ID_CURSO)
REFERENCES `CURSO` (ID_CURSO);


```
#### HAGO LAS INSERSIONES CORRESPONDIENTES PARA POBLAR LAS TABLAS

```sql
INSERT INTO `CARRERA` (`NOMBRE_CARRERA`) VALUES ('DESARROLLO DE SOFTWARE');
INSERT INTO `CARRERA` (`NOMBRE_CARRERA`) VALUES ('ELECTRONICA');
INSERT INTO `CARRERA` VALUES ('MECANICA AUTOMOTRIZ'), ('SEGURIDAD Y SALUD OCUPACIONAL'), ('SOLDADURA');

INSERT INTO `RUTA` VALUES (1,'SISTEMAS DE INFORMACION EMPRESARIALES',1),
(2,'VIDEOJUEGOS',1),
(3,'MACHINE LEARNING',1),
(4,'MICROCONTROLADORES',2),
(5,'ROBOTICA',2),
(6,'DISPOSITIVOS BIO-MEDICOS',2),
(7,'MOTORES HIBRIDOS', 3),
(8,'VEHICULOS DE USO AGRICOLA',3),
(9,'SISTEMAS DE GESTION EN SEGURIDAD OCUPACIONAL',4),
(10,'SOLDADURA AUTOGENA INDUSTRIAL',5),
(11,'SOLDADURA ELECTRICA INDUSTRIAL',5),
(12,'SOLDADURA SUBMARINA',5);

INSERT INTO `INSTRUCTOR` VALUES (1,'RICARDO VIICENTE', 'JAIMES', 'SISTEMAS'),
(2,'MARINELA','NARVAEZ', 'SALUD OCUPACIONAL'),
(3,'AGUSTIN', 'PARRA GRANADOS', 'SOLDADURA'),
(4,'NELSON RAUL','BUITRAGO','MECANICA'),
(5,'ROY HERNANDO','LLAMAS','INGLES'),
(6,'MARIA JIMENA','MONSALVE','ELECTRONICA'),
(7,'JUAN CARLOS', 'COBOS', 'ELECTRONICA'),
(8,'PEDRO NELL','SANTAMARIA', 'SISTEMAS'),
(9,'ANDREA','GONZALEZ','SISTEMAS'),
(10,'MARISELA','SEVILLA','SALUD OCUPACIONAL');

INSERT INTO `CURSO` VALUES (1,'MATEMATICAS BASICA'),
(2,'ALGEBRA COMPUTACIONAL'),
(3,'PROGRAMACION BASICA'),
(4,'INGLES'),
(5,'ELECTRONICA BASICA'),
(6,'MOTOR DE CUATRO TIEMPOS'),
(7,'ENFERMEDADES LABORALES'),
(8,'HIGIENE POSTURA'),
(9,'ERGONOMIA'),
(10,'Legislación Laboral en Colombia'),
(11,'Materiales de Soldadura'),
(12,'Métodos de Soldadura'),
(13,'Fusión de Metales'),
(14,'BUCEO 1'),
(15,'BUCEO 2'),
(16,'RIESGO ELECTRICO'),
(17,'BASES DE DATOS RELACIONALES'),
(18,'BASES DE DATOS NO RELACIONALES'),
(19,'ELECTRONICA DIGITAL'),
(20,'MICROPROCESADORES');

INSERT INTO `RUTAS_X_CURSO` VALUES (1,17,'30 HORAS'),
(1,2,'40 HORAS'),
(1,3,'30 HORAS'),
(1,18,'30 HORAS'),
(1,1,'40 HORAS'),
(1,4,'30 HORAS'),
(3,2,'40 HORAS'),
(3,4,'30 HORAS'),
(3,17,'30 HORAS'),
(4,5,'40 HORAS'),
(4,19,'40 HORAS'),
(4,20,'30 HORAS'),
(5,5,'40 HORAS'),
(5,19,'40 HORAS'),
(5,20,'30 HORAS'),
(10,11,'30 HORAS'),
(10,14,'40 HORAS'),
(11,11,'30 HORAS'),
(11,13,'40 HORAS'),
(2,1,'40 HORAS'),
(2,2,'40 HORAS'),
(2,3,'30 HORAS'),
(2,5,'40 HORAS');

INSERT INTO `APRENDIZ` VALUES (1,'ANA MARIA','VELASQUEZ PARRA',23),
(2,'ANTONIO','CAÑATE CORTES',34),
(3,'CARLOS SAUL','GOMEZ',34),
(4,'DANIEL','SIMANCAS JUNIOR', 56),
(5,'GUSTAVO','NORIEGA ALZATE',34),
(6,'HENRY', 'SOLER VEGA',23),
(7,'JAIRO AUGUSTO', 'CASTRO CAMARGO',22),
(8,'JUAN JOSE', 'CARDONA',25),
(9,'LEYLA MARIA', 'DELGADO VARGAS',26),
(10,'PEDRO NELL','GOMEZ DIAZ',20),
(11,'SERGIO AUGUSTO', 'CONTRERAS NAVAS',24);

INSERT INTO `MATRICULA` VALUES (1,1,3, 17,'ACTIVO'),
(2,1,3,2,'ACTIVO'),
(3,1,3,3,'ACTIVO'),
(4,1,3,18,'ACTIVO'),
(5,1,9,1,'ACTIVO'),
(6,1,9,2,'ACTIVO'),
(7,1,9,3,'ACTIVO'),
(8,1,9,4,'ACTIVO'),
(9,2,8,1,'CANCELADO'),
(10,2,8,2,'CANCELADO'),
(11,2,8,3,'CANCELADO'),
(12,2,11,4,'ACTIVO'),
(13,2,11,1,'ACTIVO'),
(14,2,11,2,'ACTIVO'),
(15,3,1,3,'ACTIVO'),
(16,3,1,4,'ACTIVO'),
(17,3,1,17,'ACTIVO'),
(18,4,5,5,'TERMINADO'),
(19,4,5,19,'TERMINADO'),
(20,4,5,20,'TERMINADO'),
(21,4,10,5,'TERMINADO'),
(22,4,10,19,'TERMINADO'),
(23,4,10,20,'TERMINADO'),
(24,5,7,5,'TERMINADO'),
(25,5,7,19,'TERMINADO'),
(26,5,6,5,'CANCELADO'),
(27,5,6,19,'CANCELADO'),
(28,5,6,20,'CANCELADO'),
(29,11,2,11,'TERMINADO'),
(30,11,2,13,'TERMINADO'),
(31,10,4,11,'TERMINADO'),
(32,10,4,14,'TERMINADO');

INSERT INTO CURSO_INSTRUCTOR VALUES
(1,4),
(2,1),
(3,3),
(4,5),
(5,7),
(6,NULL),
(7,NULL),
(8,NULL),
(9,NULL),
(10,NULL),
(11,3),
(12,NULL),
(13,3),
(14,NULL),
(15,NULL),
(16,NULL),
(17,2),
(18,2),
(19,6),
(20,7);

```

### Consultas

1. Agregue un campo Estado_Matrícula a la tabla Matrícula que indique si el estudiante se encuentra “En Ejecución”, “Terminado” o “Cancelado”

   Se adiciona la columna 'ESTADO' con la especificacion requerida.

   ```sql
    	ALTER TABLE `MATRICULA` ADD ESTADO VARCHAR(15)
   ```

   Validacion de la tabla:
   
   ```bash
	+--------------+-------------+------+-----+---------+----------------+
	| Field        | Type        | Null | Key | Default | Extra          |
	+--------------+-------------+------+-----+---------+----------------+
	| ID_MATRICULA | int         | NO   | PRI | NULL    | auto_increment |
	| ID_RUTA      | int         | YES  | MUL | NULL    |                |
	| ID_APRENDIZ  | int         | NO   | MUL | NULL    |                |
	| ID_CURSO     | int         | YES  | MUL | NULL    |                |
	| ESTADO       | varchar(15) | YES  |     | NULL    |                |
	+--------------+-------------+------+-----+---------+----------------+

   ```
   
2. Agregue a el campo edad a la tabla de Aprendices.

   Se adiciona la columna 'EDAD' con la especificacion requerida.

   ```sql
      	ALTER TABLE `APRENDIZ` ADD EDAD INT;
   ```

   Validacion de la tabla:
   
   ```bash
	+-------------------+-------------+------+-----+---------+----------------+
	| Field             | Type        | Null | Key | Default | Extra          |
	+-------------------+-------------+------+-----+---------+----------------+
	| ID_APRENDIZ       | int         | NO   | PRI | NULL    | auto_increment |
	| NOMBRE_APRENDIZ   | varchar(20) | YES  |     | NULL    |                |
	| APELLIDO_APRENDIZ | varchar(20) | YES  |     | NULL    |                |
	| EDAD              | int         | YES  |     | NULL    |                |
	+-------------------+-------------+------+-----+---------+----------------+
   ```

3. Si suponemos que los cursos tienen una duración diferente dependiendo de la ruta que lo contenga ¿qué modificación haría a la estructura de datos ya planteada?

   Se adiciona la columna 'DURACION' en la tabla RUTAS_X_CURSO

   ```sql
     	ALTER TABLE RUTAS_X_CURSO ADD DURACION VARCHAR(30)
   ```

   Validacion de la tabla:
   
   ```bash
	+----------+-------------+------+-----+---------+-------+
	| Field    | Type        | Null | Key | Default | Extra |
	+----------+-------------+------+-----+---------+-------+
	| ID_RUTA  | int         | NO   | MUL | NULL    |       |
	| ID_CURSO | int         | NO   | MUL | NULL    |       |
	| DURACION | varchar(30) | YES  |     | NULL    |       |
	+----------+-------------+------+-----+---------+-------+
   ```

4. Seleccionar los nombres y edades de aprendices que están cursando la carrera de electrónica.

   ```sql
      	SELECT  DISTINCT NOMBRE_APRENDIZ, APELLIDO_APRENDIZ, EDAD FROM `APRENDIZ`
	JOIN `MATRICULA` ON APRENDIZ.`ID_APRENDIZ` = MATRICULA.`ID_APRENDIZ`
	JOIN `RUTA` ON MATRICULA.`ID_RUTA` = RUTA.`ID_RUTA`
	JOIN `CARRERA` ON RUTA.`ID_CARRERA` = CARRERA.`ID_CARRERA`
	WHERE CARRERA.`NOMBRE_CARRERA`='ELECTRONICA';
   ```

   Resultado:

   ```bash
	+-----------------+-------------------+------+
	| NOMBRE_APRENDIZ | APELLIDO_APRENDIZ | EDAD |
	+-----------------+-------------------+------+
	| GUSTAVO         | NORIEGA ALZATE    |   34 |
	| PEDRO NELL      | GOMEZ DIAZ        |   20 |
	| JAIRO AUGUSTO   | CASTRO CAMARGO    |   22 |
	| HENRY           | SOLER VEGA        |   23 |
	+-----------------+-------------------+------+

   ```

5. Seleccionar Nombres de Aprendices junto al nombre de la ruta de aprendizaje que cancelaron.

   ```sql
      	SELECT  DISTINCT NOMBRE_APRENDIZ, APELLIDO_APRENDIZ, NOMBRE_RUTA FROM `APRENDIZ`
	JOIN `MATRICULA` ON APRENDIZ.`ID_APRENDIZ` = MATRICULA.`ID_APRENDIZ`
	JOIN RUTA ON MATRICULA.`ID_RUTA` = RUTA.`ID_RUTA`
	WHERE `ESTADO`='CANCELADO';
   ```

   Resultado:
   
   ```bash
	+-----------------+-------------------+-------------+
	| NOMBRE_APRENDIZ | APELLIDO_APRENDIZ | NOMBRE_RUTA |
	+-----------------+-------------------+-------------+
	| JUAN JOSE       | CARDONA           | VIDEOJUEGOS |
	| HENRY           | SOLER VEGA        | ROBOTICA    |
	+-----------------+-------------------+-------------+

   ```

6. Seleccionar Nombre de los cursos que no tienen un instructor asignado.

   ```sql
      	SELECT `NOMBRE_CURSO` FROM `CURSO`
	LEFT JOIN `CURSO_INSTRUCTOR` ON CURSO.`ID_CURSO` = `CURSO_INSTRUCTOR`.`ID_CURSO`
	WHERE CURSO_INSTRUCTOR.`ID_INSTRUCTOR` IS NULL;
   ```

   Resultado:
   
   ```bash
	+----------------------------------+
	| NOMBRE_CURSO                     |
	+----------------------------------+
	| MOTOR DE CUATRO TIEMPOS          |
	| ENFERMEDADES LABORALES           |
	| HIGIENE POSTURA                  |
	| ERGONOMIA                        |
	| Legislación Laboral en Colombia  |
	| Métodos de Soldadura             |
	| BUCEO 1                          |
	| BUCEO 2                          |
	| RIESGO ELECTRICO                 |
	+----------------------------------+
   ```

7. Seleccionar Nombres de los instructores que dictan cursos en la ruta de aprendizaje “Sistemas de Información Empresariales”.

   ```sql
      	SELECT DISTINCT NOMBRE_INSTRUCTOR FROM `INSTRUCTOR`
	JOIN `CURSO_INSTRUCTOR` ON INSTRUCTOR.`ID_INSTRUCTOR` = CURSO_INSTRUCTOR.`ID_INSTRUCTOR`
	JOIN `CURSO` ON CURSO_INSTRUCTOR.`ID_CURSO` = CURSO.`ID_CURSO`
	JOIN `RUTAS_X_CURSO` ON CURSO.`ID_CURSO` = RUTAS_X_CURSO.`ID_CURSO`
	JOIN `RUTA` ON RUTAS_X_CURSO.`ID_RUTA` = RUTA.`ID_RUTA`
	WHERE `NOMBRE_RUTA`= 'SISTEMAS DE INFORMACION EMPRESARIALES'
   ```

   Resultado:
   
   ```bash
	+-------------------+
	| NOMBRE_INSTRUCTOR |
	+-------------------+
	| MARINELA          |
	| RICARDO VIICENTE  |
	| AGUSTIN           |
	| MARINELA          |
	| NELSON RAUL       |
	| ROY HERNANDO      |
	+-------------------+

   ```

8. Genere un listado de todos los aprendices que terminaron una Carrera mostrando el nombre del profesional, el nombre de la carrera y el énfasis de la carrera (Nombre de la Ruta de aprendizaje)

   ```sql
     	SELECT DISTINCT NOMBRE_APRENDIZ, NOMBRE_CARRERA, NOMBRE_RUTA FROM `APRENDIZ`
	JOIN `MATRICULA` ON APRENDIZ.`ID_APRENDIZ` = MATRICULA.`ID_APRENDIZ`
	JOIN `RUTA` ON MATRICULA.`ID_RUTA`= RUTA.`ID_RUTA`
	JOIN `CARRERA` ON RUTA.`ID_CARRERA` = CARRERA.`ID_CARRERA`
	WHERE `ESTADO`='TERMINADO';
   ```

   Resultado:
   
   ```bash
	+-----------------+----------------+--------------------------------+
	| NOMBRE_APRENDIZ | NOMBRE_CARRERA | NOMBRE_RUTA                    |
	+-----------------+----------------+--------------------------------+
	| GUSTAVO         | ELECTRONICA    | MICROCONTROLADORES             |
	| PEDRO NELL      | ELECTRONICA    | MICROCONTROLADORES             |
	| JAIRO AUGUSTO   | ELECTRONICA    | ROBOTICA                       |
	| ANTONIO         | SOLDADURA      | SOLDADURA ELECTRICA INDUSTRIAL |
	| DANIEL          | SOLDADURA      | SOLDADURA AUTOGENA INDUSTRIAL  |
	+-----------------+----------------+--------------------------------+
   ```

9. Genere un listado de los aprendices matriculados en el curso “Bases de Datos Relacionales”.


   ```sql
    	SELECT DISTINCT NOMBRE_APRENDIZ FROM `APRENDIZ`
	JOIN `MATRICULA` ON APRENDIZ.`ID_APRENDIZ` = MATRICULA.`ID_APRENDIZ`
	JOIN `CURSO` ON MATRICULA.`ID_CURSO` = CURSO.`ID_CURSO`
	WHERE `NOMBRE_CURSO`= 'BASES DE DATOS RELACIONALES';
   ```

   Resultado:
   
   ```bash
	+-----------------+
	| NOMBRE_APRENDIZ |
	+-----------------+
	| CARLOS SAUL     |
	| ANA MARIA       |
	+-----------------+
   ```

10.  Nombres de Instructores que no tienen curso asignado.
   
   ```sql
	SELECT NOMBRE_INSTRUCTOR FROM `INSTRUCTOR`
	LEFT JOIN `CURSO_INSTRUCTOR` ON INSTRUCTOR.`ID_INSTRUCTOR` = CURSO_INSTRUCTOR.`ID_INSTRUCTOR`
	WHERE CURSO_INSTRUCTOR.`ID_INSTRUCTOR` IS NULL;
   ```

   Resultado:
   
   ```bash
	+-------------------+
	| NOMBRE_INSTRUCTOR |
	+-------------------+
	| PEDRO NELL        |
	| ANDREA            |
	| MARISELA          |
	+-------------------+

   ```

### Preguntas de selección multiple

1. ¿Cuál es la diferencia clave entre INNER JOIN y LEFT JOIN en MySQL?
- a) INNER JOIN devuelve todas las filas de la tabla izquierda y las coincidencias de la tabla derecha. RTA CORRECTA
- b) LEFT JOIN devuelve solo las filas que tienen coincidencias en ambas tablas.
- c) INNER JOIN devuelve solo las filas que tienen coincidencias en ambas tablas.
- d) LEFT JOIN devuelve todas las filas de la tabla izquierda y las coincidencias de la tabla derecha.


2. ¿Cuál es la diferencia entre CHAR y VARCHAR en MySQL y cuándo usarías cada uno?
- a) CHAR es de longitud variable y se utiliza para almacenar cadenas de longitud variable, mientras que VARCHAR es de longitud fija y se utiliza para almacenar cadenas de longitud fija.
- b) CHAR es variable en longitud y se utiliza para almacenar cadenas de longitud fija, mientras que VARCHAR es de longitud variable y se utiliza para almacenar cadenas de longitud variable. RTA CORREC
- c) Ambos son de longitud fija, pero CHAR se utiliza para datos alfanuméricos y VARCHAR para datos numéricos.
- d) Ambos son de longitud variable, pero CHAR se utiliza para datos numéricos y VARCHAR para datos alfanuméricos.


3. Completa la siguiente sentencia de SQL para crear una clave foránea (foreign key) en MySQL:
 	```sql
	ALTER TABLE tabla_hija
	ADD CONSTRAINT nombre_fk
	FOREIGN KEY (columna_hija) 
	REFERENCES tabla_padre(columna_padre);
   ```
- a) FOREIGN KEY (columna_padre) REFERENCES tabla_hija(columna_hija);
- b) FOREIGN KEY (columna_hija) ADD REFERENCES tabla_padre(columna_padre)
- c) ADD KEY (columna_hija) REFERENCES tabla_padre(columna_padre);
- d) FOREIGN KEY (columna_hija) REFERENCES tabla_padre(columna_padre); RTA CORRECTA


4. Pregunta: ¿Qué función se utiliza para contar el número de filas en una tabla en MySQL?
- a) AVG()
- b) SUM()
- c) COUNT()  RTA CORRECTA
- d) MAX()

