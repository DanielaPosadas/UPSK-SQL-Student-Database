# Student Database

## Preámbulo

Los comandos DDL (Data Definition Language) en SQL son fundamentales para la creación,
modificación y eliminación de objetos de base de datos. Estos comandos permiten
definir la estructura y características de las tablas, índices, vistas y otros
elementos esenciales en el diseño de una base de datos

## Objetivos de aprendizaje

### SQL

- Realizar operaciones básicas de consulta de una base de datos utilizando las cláusulas SELECT y WHERE
   
- CREATE TABLE

- INSERT

- UPDATE

- DELETE

- Primary Key

- Foreign key

- ALTER TABLE

- Comprender y utilizar cláusulas JOIN para combinar datos de múltiples tablas.

- Condensar resultados con cláusulas de agrupación de datos como GROUP BY y HAVING

- Ordernar el resultado utilizando la cláusula ORDER BY

- Trabajar con funciones de agregación como COUNT, SUM, AVG, MAX y MIN

- Constraints

### Virtual Machines

- Virtual Machines Setup

### PostgreSQL

- PostgreSQL Setup

- PostgreSQL Commands

- PostgreSQL Backup

- PostgreSQL Restore

### Shell

- Shell Scripts

- File Permissions


## Entregable

```md

# COMANDOS PARA LA TERMINAL
`\l` - Conocer las bases de datos disponibles
`\c nombre_de_la_base_de_datos` - Conectar con la base de datos
`\d` - Visualizar las tablas dentro de la base de datos
`ls` - Conocer los archivos que están en el proyecto
`cp archivo_original archivo_nuevo` - Copiar información de un archivo a otro nuevo
`rm archivo_a_eliminar` - Eliminar archivo innecesarios
`touch nombre_del_archivo.sh` - Crear un nuevo archivo sh
`chmod +x nombre_de_archivo.sh` - Dar los permisos necesarios al archivo de ejecutar scripts.

# TUTORIAL 1

## Paso 1
Imprimir en la terminal 'hello SQL'.

   `echo hello SQL`

## Paso 2
Acceder a la base de datos de PostgreSQL para ejecutar consultas SQL, scripts y comandos de administración.
   `psql --username=freecodecamp --dbname=psql`

## Paso 3
Para visualizar en la terminal la lista de bases de datos disponibles.
   `\l`

## Paso 4
Crear nuestra base de datos llamada 'students'
   `CREATE DATABASE students`

## Paso 5
Conectar con nuestra base de datos 'students'
   `\c students`

## Paso 6
Crear la primer tabla 'students' con las columnas 'first_name', 'last_name',
'major', 'gpa' y sus tipos de datos text y decimal.
   `CREATE TABLE students (first_name text, last_name text, major text, gpa decimal)`

## Paso 7
Crear la segunda tabla 'majors' con la columna 'major' y sus tipo de dato text.
   `CREATE TABLE majors (major text)`

## Paso 8
Crear la tercer tabla 'courses' con la columna 'course' y sus tipo de dato text.
   `CREATE TABLE courses (course text)`

## Paso 9
Crear la cuarta tabla 'majors_courses' sin ninguna columna y tipo de dato por ahora,
pues será una intersección entre major y courses.
   `CREATE TABLE majors_courses()`

## Paso 10
Visualizar las tablas presentes en nuestra base de datos 'students'.
   `\d`

## Paso 11
Agregar a la tabla ya existente 'students' una columna llamada 'students_id' con
el tipo SERIAL PRIMARY KEY para generar secuencialmente identificadores únicos.
   `ALTER TABLE students ADD COLUMN student_id SERIAL PRIMARY KEY`

## Paso 12
Elimina las columnas ya creadas en las tablas existentes para modificar su tipo
de dato. Crea nuevamente la columna y asigna el nuevo tipo de dato en cada una:

   `ALTER TABLE students DROP COLUMN first_name`
   `ALTER TABLE students ADD COLUMN first_name VARCHAR(50) NOT NULL` --Antes text

   `ALTER TABLE students DROP COLUMN last_name`
   `ALTER TABLE students ADD COLUMN last_name VARCHAR(50) NOT NULL` --Antes text

   `ALTER TABLE students DROP COLUMN gpa`
   `ALTER TABLE students ADD COLUMN gpa NUMERIC(2,1);` --Antes decimal
   
   `ALTER TABLE majors DROP COLUMN major`
   `ALTER TABLE majors ADD COLUMN major VARCHAR(50) NOT NULL` --Antes text
   
   `ALTER TABLE courses DROP COLUMN course`
   |`ALTER TABLE courses ADD COLUMN course VARCHAR(100) NOT NULL`  --Antes text

## Paso 13
Agrega una nueva columna llamada 'major_id' a nuestra tabla students con tipo de dato INT.
Más adelante se le asignará el valor foreign key para relacionarla con otra tabla.
   `ALTER TABLE students ADD COLUMN major_id INT`

## Paso 14
Agrega a la tabla ya existente 'majors' una columna llamada 'major_id' con el tipo de dato
SERIAL PRIMARY KEY para generar secuencialmente identificadores únicos.
   `ALTER TABLE majors ADD COLUMN major_id SERIAL PRIMARY KEY`

## Paso 15
Agrega una clave foránea en students para relacionar la tabla students y majors a través
de la columna major_id que existe en ambas.
   `ALTER TABLE students ADD FOREIGN KEY (major_id) REFERENCES majors (major_id)`

## Paso 16
Agrega a la tabla ya existente 'courses' una columna llamada 'course_id' con el tipo de
dato SERIAL PRIMARY KEY para generar secuencialmente identificadores únicos.
   `ALTER TABLE courses ADD COLUMN course_id SERIAL PRIMARY KEY`

## Paso 17
Agrega a la tabla ya existente 'majors_courses' una columna llamada 'major_id' con el tipo de dato INT.
   `ALTER TABLE majors_courses ADD COLUMN major_id INT`

## Paso 18
Agrega una clave foránea en majors_courses para relacionar la tabla majors_courses y majors a través
de la columna major_id que existe en ambas.
   `ALTER TABLE majors_courses ADD FOREIGN KEY (major_id) REFERENCES majors (major_id)`

## Paso 19
Agrega a la tabla ya existente 'majors_courses' una columna llamada 'course_id' con el tipo de dato INT.
   `ALTER TABLE majors_courses ADD COLUMN course_id INT`

## Paso 20
Agrega una clave foránea en majors_courses para relacionar la tabla majors_courses y courses a través
de la columna course_id que existe en ambas.
   `ALTER TABLE majors_courses ADD FOREIGN KEY (course_id) REFERENCES courses(course_id)`

## Paso 21
Agrega una clave primaria compuesta en majors_courses para crear valores únicos al combinar la columna courses_id y majors_id.
   `ALTER TABLE majors_courses ADD PRIMARY KEY (course_id, major_id)`

##INSERTAR DATOS A LAS TABLAS CREADAS

## Paso 1
Agrega los primeros datos a la tabla majors en la columna major, siempre y cuando sea texto debido al
tipo de dato que acepta esta columna. Luego visualiza toda la información dentro de la tabla majors.
   `INSERT INTO majors(major) VALUES ('Database Administration')`
   `SELECT * FROM majors`

## Paso 2
Agrega los primeros datos a la tabla courses en la columna course, siempre y cuando sea texto debido al
tipo de dato que acepta esta columna. Luego visualiza toda la información dentro de la tabla courses.
   `INSERT INTO courses(course) VALUES ('Data Structures and Algorithms')`
   `SELECT * FROM courses`

## Paso 3
Agrega los primeros datos a la tabla majors_courses. En este caso ambos esperan un número entero que pertenece
al id de course y de major, al ser los primeros datos de ambas tablas, se asigna el número 1.
   `INSERT INTO majors_courses(course_id, major_id) VALUES (1,1)`
   `SELECT * FROM majors_courses`

## Paso 4
Agrega los primeros datos a la tabla students.
   `INSERT INTO students(first_name, last_name, major, gpa, major_id) VALUES ('Rhea','Kellems','Database Administration', 2.5, 1)`
   `SELECT * FROM students`

##CREAR UN ARCHIVO SH NUEVO PARA EJECUTAR SCRIPTS

## Paso 1
Crea un nuevo archivo insert_data.sh el cual permitirá estructurar scripts para insertar la data de nuestros archivos
a las tablas de la base de datos de una forma más óptima.
   `touch insert_data.sh`

## Paso 2
Agrega un comando a la terminal para conceder permisos al archivo .sh de ejecutar scripts.
   `chmod +x insert_data.sh`

## Paso 3
En el nuevo archivo .sh debe colocar un marcador especial llamado shebang que indica al sistema qué programa debe usarse para interpretar el archivo.

   `#!/bin/bash` --Se coloca al inicio del archivo insert_data.sh`

## Paso 4
Agregar debajo del shebang un comentario:
   #!/bin/bash
   `#Script to insert data from courses.csv and students.csv into students database`

## Paso 5
Agregar debajo del comentario este comando de terminal para que muestre la información de nuestro archivo courses.csv.
   #!/bin/bash
   #Script to insert data from courses.csv and students.csv into students database
   `cat courses.csv`

## Paso 6
Colocamos en la terminal un comando para que ejecute en la terminal el script del archivo .sh.
   `./insert_data.sh`
Imprimiendo en la terminal la información del archivo courses.csv:
   major,course
   Database Administration,Data Structures and Algorithms
   Web Development,Web Programming
   Database Administration,Database Systems
   Data Science,Data Structures and Algorithms
   ...

## Paso 7
Complementa el cat courses.csv para que ejecute un bucle while y asigne valores a las variables course y major a través del espacio en blanco.
   `cat courses.csv | while read MAJOR COURSE`
	`do`
  	`<STATEMENTS>`
	`done`
   Ej: Línea: Math Algebra
         - MAJOR será Math
         - COURSE será Algebra

## Paso 8
Dentro de los statements de nuestro bucle while imprime los valores de la variable MAJOR al ejecutar línea por línea.
   `cat courses.csv | while read MAJOR COURSE`
	`do`
  	   `echo $MAJOR`
	`done`
Imprime en la terminal:
   major,course
   Database
   Web
   Database
   Data
   Network
   ...

## Paso 9
Ejecuta un comando en la terminal que define los caracteres que se utilizarán para dividir una cadena en campos cuando se leen datos.
   `declare -p IFS`

## Paso 10
Indicamos en el script que el caracter separados será una coma (,), entonces el primer valor de MAJOR será todo lo que se encuentre antes del caracter separador, en este caso, una coma.
   `cat courses.csv | while IFS="," read MAJOR COURSE`

## Paso 11
Imprime ambas variables en la terminal.
   `cat courses.csv | while read MAJOR COURSE`
	`do`
  	   `echo $MAJOR $COURSE`
	`done`

## Paso 12
Agrega una variable antes del loop para consultar la base de datos desde el script.
   `PSQL="psql -X --username=freecodecamp --dbname=students --no-align --tuples-only -c"`

## Paso 13
Agregamos una variable para recuperar el major_id de nuestra base de datos, que en este caso se creará automáticamente por el tipo de dato que le dimos (SERIAL PRIMARY KEY). Agregamos un echo para imprimir el resultado en la terminal.
   #!/bin/bash
   #Script to insert data from courses.csv and students.csv into students database
   PSQL="psql -X --username=freecodecamp --dbname=students --no-align --tuples-only -c"
   cat courses.csv | while IFS="," read MAJOR COURSE
   do
   #get major_id
   `MAJOR_ID=$($PSQL "SELECT major_id FROM majors WHERE major='$MAJOR'")`
   `echo $MAJOR_ID`
   done

## Paso 14
Agregamos un if para que ejecute statements si la variable MAJOR está vacía (-z verifica si la variable está vacía o no).
Si MAJOR_ID está vacía, se asigna el valor guardado en $MAJOR a la columna major de la tabla majors.
   `if [[ -z $MAJOR_ID ]]`
   then
      #insert major
   INSERT_MAJOR_RESULT=$($PSQL "INSERT INTO majors(major) VALUES('$MAJOR')")
      #get new major_id
   fi

## Paso 15
Crea una copia del archivo courses.csv para hacer pruebas. Utiliza el comando cp en la terminal.
   `cp courses.csv courses_test.csv`

## Paso 16
Utilizamos truncate para eliminar toda la información de nuestra tabla majors y courses. Al tener foreign keys, utilizamos truncate en todas las tablas que están relacionadas.
   `TRUNCATE majors`
   `TRUNCATE majors, majors_courses, students`
   `TRUNCATE courses`
   `TRUNCATE courses, majors_courses`

## Paso 17
Agrega un if al inicio del loop para verificar que el valor guardado en la variable $MAJOR no sea igual a la cadena "major". De esta forma el título de la información no se integrará a nuestras columnas.
   `if [[ $MAJOR != major ]]`

## Paso 18
Agrega un if más para verificar que los valores que se hayan insertado en las tablas sean los correctos mostrando un mensaje.
   INSERT_MAJOR_RESULT=$($PSQL "INSERT INTO majors(major) VALUES('$MAJOR')")
    `if [[ $INSERT_MAJOR_RESULT == "INSERT 0 1" ]]`
      `then`
      `echo "Inserted into majors, $MAJOR"`
      `fi`

## Paso 19
Agrega la variable MAJOR_ID nuevamente para que se le asigne el ID recuperado de INSERT_MAJOR_RESULT.
   if [[ -z $MAJOR_ID ]]
      then
      #insert major
       INSERT_MAJOR_RESULT=$($PSQL "INSERT INTO majors(major) VALUES('$MAJOR')")
       if [[ $INSERT_MAJOR_RESULT == "INSERT 0 1" ]]
            then
            echo "Inserted into majors, $MAJOR"
            fi
      #get new major_id
      `MAJOR_ID=$($PSQL "INSERT INTO majors(major) VALUES('$MAJOR')")`
   fi

## Paso 20
Repetimos los mismo paso para la variable $COURSE y la tabla courses.

## Paso 21
Agrega un script que nos permita eliminar todas las filas de nuestras columnas sin necesidad de hacerlo manual.
`echo $($PSQL "TRUNCATE students, majors, courses, majors_courses")`

## Paso 22
Finalmente agrega a la tabla major_courses los valores de las variables $MAJOR y $COURSE. Verifica si la inserción fue exitosa
y muestra un mensaje en la terminal.
   `#insert into majors_courses`
   `INSERT_MAJORS_COURSES_RESULT=$($PSQL "INSERT INTO majors_courses(major_id, course_id) VALUES($MAJOR_ID, $COURSE_ID)")`
   `if [[ $INSERT_MAJORS_COURSES_RESULT == "INSERT 0 1" ]]`
   `then`
      `echo Inserted into majors_courses, $MAJOR : $COURSE`
    `fi`

## Paso 23
Crea una copia del archivo students.csv para realizar el mismo proceso.
   `cp students.csv students_test.csv`

## Paso 24
Repite el mismo proceso, sin embargo realiza una condición donde si el valor de la variable $MAJOR_ID está vacío entonces que se le asigne un valor nulo. Debe asignar de esta forma los valores línea por línea a las variables FIRST, LAST, MAJOR y GPA.
      `cat students_test.csv | while IFS="," read FIRST LAST MAJOR GPA`
      `do`
         `if [[ $FIRST != "first_name" ]]`
              `then`
                `#get major_id`
                `MAJOR_ID=$($PSQL "SELECT major_id FROM majors WHERE major='$MAJOR'") `
                  `#if not found`
                `if [[ -z $MAJOR_ID ]]`
                `then`
                `#set to null`
                  `MAJOR_ID=null`
                `fi`
                `#insert student`
                 `INSERT_STUDENT_RESULT=$($PSQL "INSERT INTO students(first_name, last_name, major_id, gpa)`
                  `VALUES('$FIRST', '$LAST',$MAJOR_ID, $GPA)")`
         `fi`
      `done`

## Paso 25
1. Visualizar qué archivos forman parte de mi proyecto y 2. Eliminar los que ya no necesito.
   `ls`
   `rm students_test.csv`
   `rm courses_test.csv`

## Paso 26
Hemos terminado la base de datos, por que lo se debe colocar en la terminal un comando para crear un archivo SQL llamado students.sql.
   `pg_dump --clean --create --inserts --username=freecodecamp students > students.sql`




# TUTORIAL 2

## Paso 1
Para inicializar la terminal.
   `echo hello SQL`

## Paso 2
Para acceder a psql.
   `psql --username=freecodecamp --dbname=postgres`

## Paso 3
Abrir una segunda terminal para traer la base de datos sql.
   `psql -U postgres < students.sql`

## Paso 4
Consultar todas las bases de datos existentes.
   `\l`

## Paso 5
Conectar con la base de datos students.
   `\c students`

## Paso 6
Mostrar las columnas que tiene nuestra tabla students.
   `\d students`

## Paso 7
Mostrar toda la información de nuestra tabla students.
   `SELECT * FROM students;`

## Paso 8
Para visualizar la columna de nombres de la tabla students.
   `SELECT first_name FROM students;`

## Paso 9
Realizar diferentes consultas a nuestra tabla students:
   `SELECT first_name, last_name, gpa FROM students;`
   `SELECT first_name, last_name, gpa FROM students WHERE gpa < 2.5;`
   `SELECT first_name, last_name, gpa FROM students WHERE gpa >= 3.8;`
   `SELECT first_name, last_name, gpa FROM students WHERE gpa != 4.0;`

Visualizar todas las columnas de la tabla students que tengan last_name antes de la letra M.
   `SELECT * FROM students WHERE last_name < 'M';`

Visualizar todas las columnas de la tabla students que tengan last_name antes de la letra M o que tengan un gpa igual a 3.9 	(alguna de las dos condiciones es verdadera, no ambas):
   `SELECT * FROM students WHERE last_name < 'M' OR gpa = 3.9;`

Visualizar todas las columnas de la tabla students que tengan last_name antes de la letra M o que tengan un gpa igual a 3.9 	(ambas condiciones son verdaderas).
   `SELECT * FROM students WHERE last_name < 'M' AND  gpa = 3.9;`

Visualizar todas las columnas de la tabla students que tengan last_name antes de la letra M o que tengan un gpa igual a 3.9 o menor a 2.3 (aquí las tres condiciones se cumplen de cierta forma).
   `SELECT * FROM students WHERE last_name < 'M' AND  gpa = 3.9 OR gpa < 2.3;`

Visualizar todas las columnas de la tabla students que tengan last_name antes de la letra M y que tengan un gpa igual a 3.9 o menor a 2.3 (aquí sólo se cumplen dos condiciones, que la letra sea antes de la M y que su gpa sea igual a 3.9 o menor a 2.3).
   `SELECT * FROM students WHERE last_name < 'M' AND  (gpa = 3.9 OR gpa < 2.3);`

Visualizar las filas de estudiantes donde su gpa tenga un valor NULL, es decir, que no contenga nada.
   `SELECT * FROM students WHERE gpa IS NULL;`

Visualizar las filas de estudiantes donde su gpa tenga NO TENGA valor NULL, es decir, que sí tenga un valor.
   `SELECT * FROM students WHERE gpa IS NOT NULL;`

Visualizar a los estudiantes que no han elegido una carrera.
   `SELECT * FROM students WHERE major_id IS NULL;`

Visualizar a los estudiantes que no han elegido una carrera, pero no incluir a los que no tienen un gpa.
   `SELECT * FROM students WHERE major_id IS NULL AND gpa IS NOT NULL;`

Visualizar a los estudiantes que no han elegido una carrera y no tienen un gpa.
   `SELECT * FROM students WHERE major_id IS NULL AND gpa IS NULL;`

Ordenar las gpa de manera ascendente.
   `SELECT * FROM students ORDER BY gpa;`

Ordenar las gpa de manera ascendente.
   `SELECT * FROM students ORDER BY gpa DESC;`

Ordenar las gpa de mayor a menor y a su vez el first_name de manera ascendente.
   `SELECT * FROM students ORDER BY gpa DESC, first_name;`

Ordenar las gpa de mayor a menor y a su vez el first_name de manera ascendente, agregando un límite de 10.
   `SELECT * FROM students ORDER BY gpa DESC, first_name LIMIT 10;`

Excluir a los estudiantes que NO tiene gpa, luego ordenar las gpa de mayor a menor y a su vez el first_name de manera ascendente, agregando un límite de 10.
   `SELECT * FROM students WHERE gpa IS NOT NULL ORDER BY gpa DESC, first_name LIMIT 10;`

Seleccionar el valor más bajo de gpa en la tabla estudiantes.
   `SELECT MIN(gpa) FROM students;`

Seleccionar el valor más alto de gpa en la tabla estudiantes.
   `SELECT MAX(gpa) FROM students;`

Devuelve la suma total de todos los valores en la columna major_id.
   `SELECT SUM(major_id) FROM students;`

Devuelve el promedio de todos los valores en la columna major_id.
   `SELECT AVG(major_id) FROM students;`

Redondea el valor del promedio hacia arriba (CEIL), al entero más cercano. No importa si la parte decimal es menor de 0.5; siempre redondeará hacia arriba.
   `SELECT CEIL(AVG(major_id)) FROM students;`

Si la parte decimal es 0.5 o mayor (ROUND), redondeará hacia arriba; si es menor de 0.5, redondeará hacia abajo.
   `SELECT ROUND(AVG(major_id)) FROM students;`

Podemos indicarle el número de decimales que queremos luego del punto, en este caso son 5 decimales.
   `SELECT ROUND(AVG(major_id), 5) FROM students;`

Devuelve la cantidad de majors (filas) dentro de nuestra tabla majors.
   `SELECT COUNT(*) FROM majors;`

Devuelve la cantidad de estudiantes dentro de la tabla students.
   `SELECT COUNT(*) FROM students;`

Devuelve cuántos estudiantes seleccionaron una carrera en la tabla students.
   `SELECT COUNT(major_id) FROM students;`

Devuelve los valores únicos de major_id de la tabla students sin repetirlos.
   `SELECT DISTINCT(major_id) FROM students;`

Devuelve los valores únicos de major_id de la tabla students agrupándolos, de esta manera son únicos.
   `SELECT major_id FROM students GROUP BY major_id;`

Devuelve los valores correspondientes a la columna major_id contando cuántos estudiantes pertenecen a ése major agrupándolo con un GROUP BY y devolviendo valores únicos.
   `SELECT major_id, COUNT(*) FROM students GROUP BY major_id;`

Devuelve los valores correspondientes a la columna major_id, además de los valores mínimos del gpa en cada major, agrupándolo con un GROUP BY y devolviendo valores únicos.
   `SELECT major_id, MIN(gpa) FROM students GROUP BY major_id;`

Devuelve los valores correspondientes a la columna major_id, además de los valores mínimos  y máximos del gpa en cada major, agrupándolo con un GROUP BY y devolviendo valores únicos.
   `SELECT major_id, MIN(gpa), MAX(gpa) FROM students GROUP BY major_id;`

Devuelve los valores correspondientes a la columna major_id, además de los valores mínimos  y máximos del gpa en cada major, agrupándolo con un GROUP BY y devolviendo valores únicos. Finalmente agrega una última condición devolviendo sólo los que tengan un gpa igual a 4.0.
   `SELECT major_id, MIN(gpa), MAX(gpa) FROM students GROUP BY major_id HAVING MAX(gpa) = 4.0;`

Devuelve los valores correspondientes a la columna major_id, además de los valores mínimos  y máximos del gpa en cada major, agrupándolo con un GROUP BY y devolviendo valores únicos. Finalmente agrega una última condición devolviendo sólo los que tengan un gpa igual a 4.0. El cambio aquí es que renombre la columna min(gpa) a min_gpa.
   `SELECT major_id, MIN(gpa) as min_gpa, MAX(gpa) FROM students GROUP BY major_id HAVING MAX(gpa) = 4.0;`

Devuelve los valores correspondientes a la columna major_id, además de los valores mínimos  y máximos del gpa en cada major, agrupándolo con un GROUP BY y devolviendo valores únicos. Finalmente agrega una última condición devolviendo sólo los que tengan un gpa igual a 4.0. El cambio aquí es que renombre la columna max(gpa) a max_gpa.
   `SELECT major_id, MIN(gpa) as min_gpa, MAX(gpa) as max_gpa FROM students GROUP BY major_id HAVING MAX(gpa) = 4.0;`

Devuelve la columna major_id y el número de estudiantes en cada major renombrado la columna como number_of_students, el major_id lo agrupa con group by.
   `SELECT major_id, COUNT(*) as number_of_students FROM students GROUP BY major_id;`

Devuelve la columna major_id y el número de estudiantes en cada major renombrado la columna como number_of_students, el major_id lo agrupa con group by, agregando un último filtro con having donde sólo se muestren las filas con un numero de estudiantes menor a 8.
   `SELECT major_id, COUNT(*) as number_of_students FROM students GROUP BY major_id HAVING COUNT(*) < 8;`

Uniendo ambas tablas (students y majors) con la foreign key que es major_id. Usando FULL JOIN se unen ambas tablas ya sea que tengan o no una fila que use esa clave externa en la otra, es decir, que alguna de las filas este vacía.
   `SELECT * FROM students FULL JOIN majors ON students.major_id = majors.major_id;`

En este caso sólo muestra todas las filas de la tabla de la derecha, en este caso de students, y omite las filas vacías o nulas de la tabla de la derecha, es decir, majors.
   `SELECT * FROM students LEFT JOIN majors ON students.major_id = majors.major_id;`

En este caso sólo muestra todas las filas de la tabla de la derecha, en este caso de majors, y omite las filas vacías o nulas de la tabla de la izquierda, es decir, students.
   `SELECT * FROM students RIGHT JOIN majors ON students.major_id = majors.major_id;`

Aquí sólo devuelve la información que esté presente en ambas tablas.
   `SELECT * FROM students INNER JOIN majors ON students.major_id = majors.major_id;`

Muestra todos los majors, pero NO muestra a los estudiantes que no tienen un major.
   `SELECT * FROM majors LEFT JOIN students ON majors.major_id = students.major_id;`

Devuelve los estudiantes que están inscritos o tiene un major y los majors que tienen estudiantes:
   `SELECT * FROM students INNER JOIN majors ON students.major_id= majors.major_id;`

Muestra a todos los estudiantes, pero no devuelve todos los majors vacíos.
   `SELECT * FROM majors RIGHT JOIN students ON majors.major_id = students.major_id;`

Devuelve todas las filas de cada tabla, estén vacías o no.
   `SELECT * FROM majors FULL JOIN students ON majors.major_id = students.major_id;`

Devuelve todos los majors a los que pertenecen los estudiantes uniendo ambas tablas.
   `SELECT * FROM students INNER JOIN majors ON students.major_id = majors.major_id;`

Devuelve la columna major de la tabla majors aplicando un INNER JOIN para unir ambas tablas por la columna major_id.
   `SELECT major FROM majors INNER JOIN students ON students.major_id = majors.major_id;`

Devuelve los valores únicos de majors sin repetirlos utilizando DISTINCT.
   `SELECT DISTINCT(major) FROM majors INNER JOIN students ON students.major_id = majors.major_id;`

Devuelve todas las columnas de los estudiantes que tienen un major.
   `SELECT * FROM students RIGHT JOIN majors ON majors.major_id = students.major_id;`

Devuelve todas las columnas de los majors que no tengan estudiantes inscritos.
   `SELECT * FROM students RIGHT JOIN majors ON majors.major_id = students.major_id WHERE student_id IS NULL;`

Devuelve sólo la columna major de los que no tienen estudiantes inscritos.
   `SELECT major FROM majors LEFT JOIN students ON majors.major_id = students.major_id WHERE student_id IS NULL`

Devuelve los estudiantes inscritos a un major.
   `SELECT * FROM students LEFT JOIN majors ON students.major_id = majors.major_id;`

Devuelve los estudiantes que estén inscritos en el major Data Science o tengan un gpa igual o mayor a 3.8.
   `SELECT * FROM students LEFT JOIN majors ON students.major_id = majors.major_id WHERE major = 'Data Science' OR gpa >= 3.8;`

Utiliza un FULL JOIN para unir las tablas students y majors devolviendo todas las columnas de ambas tablas.
   `SELECT * FROM students FULL JOIN majors ON students.major_id = majors.major_id;`

Retoma la query anterior e implementa un LIKE para buscar los majors o first_name que contengan ‘ri’.
   `SELECT * FROM students FULL JOIN majors ON students.major_id = majors.major_id WHERE first_name LIKE '%ri%' OR major LIKE
   '%ri%';`

Retoma el query anterior y selecciona únicamente la columna first_name y major.
   `SELECT first_name, major FROM students FULL JOIN majors ON students.major_id = majors.major_id WHERE first_name LIKE '%ri%' OR
   major LIKE '%ri%';`

Devuelve todas las filas de las tablas students y majors con un FULL JOIN.
   `SELECT * FROM students FULL JOIN majors ON students.major_id = majors.major_id;`

Devuelve la columna major_id de la tabla students.
   `SELECT students.major_id FROM students FULL JOIN majors ON students.major_id = majors.major_id;`

Renombra la tabla majors como ‘m’ y hace un FULL JOIN utilizando la tabla renombrada m.major_id.
   `SELECT students.major_id FROM students FULL JOIN majors AS m ON students.major_id = m.major_id;`

Renombra la tabla students como ‘s’ y hace un FULL JOIN utilizando la tabla renombrada s.major_id.
   `SELECT s.major_id FROM students AS s FULL JOIN majors AS m ON s.major_id = m.major_id;`

Devuelve la tabla students y majors pero utiliza un USING(foreign key de ambas tablas) para unirlas y hacer el query más simple.
   `SELECT * FROM students FULL JOIN majors USING(major_id);`

Unir tres tablas con el uso de USING y la foreign key major_id.
   `SELECT * FROM students FULL JOIN majors USING(major_id) FULL JOIN majors_courses USING(major_id);`

Devuelve los resultados de las cuatro tablas students, majors, majors_courses y courses utilizando USING y FULL JOIN.
   `SELECT * FROM students FULL JOIN majors USING(major_id) FULL JOIN majors_courses USING(major_id) FULL JOIN courses
    USING(course_id);`

## Paso 10
Para visualizar la columna de nombres de la tabla majors.
   `SELECT * FROM majors;`

## Paso 11
Realizar diferentes consultas a nuestra tabla majors:
   `SELECT * FROM majors WHERE major  = 'Game Design';`

Visualizar los majors que no tengan el nombre ‘Game Design’.
   `SELECT * FROM majors WHERE major != 'Game Design';`

Visualizar valores en la columna major que están después de 'Game Design' en orden alfabético.
   `SELECT * FROM majors WHERE major > 'Game Design';`

Visualizar valores en la columna major que están después de 'Game Design' en orden alfabético, incluso el mismo Game Design.
   `SELECT * FROM majors WHERE major >= 'Game Design';`

Visualizar valores en la columna major que están antes de la letra ‘G’.
   `SELECT * FROM majors WHERE major < 'G';`

## Paso 10
Visualizar toda la información de la tabla courses:.
   `SELECT * FROM courses;`

## Paso 11
Realizar diferentes consultas a nuestra tabla courses.

Visualizar todas las columnas de la tabla courses utilizando LIKE para localizar los courses que tengan en el nombre el primer caracter, seguido de ‘lgorithms’ en el nombre.
   `SELECT * FROM courses WHERE course LIKE '_lgorithms';`

Visualizar los courses que terminen con ‘logarithms’.
   `SELECT * FROM courses WHERE course LIKE '%lgorithms';`

Visualizar los courses que empiecen con ‘Web’.
   `SELECT * FROM courses WHERE course LIKE 'Web%’;`

Visualizar los courses donde el segundo caracter sea una ‘e’.
   `SELECT * FROM courses WHERE course LIKE '_e%';`

Visualizar los courses que contengan un espacio en el nombre.
   `SELECT * FROM courses WHERE course LIKE '% %';`

Visualizar los courses que NO contengan un espacio en el nombre.
   `SELECT * FROM courses WHERE course NOT LIKE '%  %';`

Visualizar los courses que contengan una ‘A’ en el nombre (A mayúscula).
   `SELECT * FROM courses WHERE course LIKE '%A%';`

Visualizar los courses que contengan una ‘A’ en el nombre (ILIKE permite ignorar el capital case, en este caso es tanto alta como baja ‘A’ o ‘a’).
   `SELECT * FROM courses WHERE course ILIKE '%A%';`

Visualizar los courses que NO contengan una ‘A’ en el nombre (ILIKE permite ignorar el capital case, en este caso es tanto alta como baja ‘A’ o ‘a’).
   `SELECT * FROM courses WHERE course NOT ILIKE '%A%';`

Visualizar los courses que NO contengan una ‘A’ en el nombre (ILIKE permite ignorar el capital case, en este caso es tanto alta como baja ‘A’ o ‘a’) y contengan un espacio.
   `SELECT * FROM courses WHERE course NOT ILIKE '%A%' AND course LIKE '%  %';`

Visualizar los courses que NO contengan una ‘A’ en el nombre (ILIKE permite ignorar el capital case, en este caso es tanto alta como baja ‘A’ o ‘a’) y contengan un espacio.
   `SELECT * FROM courses WHERE course NOT ILIKE '%A%' AND course LIKE '%  %';`

# CREAR UN ARCHIVO SH PARA EJECUTAR SCRIPTS

## Paso 1
En una split terminal crear un archivo .sh para anotar scripts.
   `touch student_info.sh`

## Paso 2
Dar los permisos necesarios para ejecutar scripts a mi archivo sh.
   `chmod +x student_info.sh`

## Paso 3
Colocar el shebang para que permita ejecutar los scripts en el nuevo archivo sh.
   `#!/bin/bash`

## Paso 4
Agregamos un comentario en nuestro archivo .sh y corremos el comando para visualizarlo en la terminal.
   `echo -e "\n~~ My Computer Science Students ~~\n"`

## Paso 5
Agregar variable PSQL.
   `PSQL="psql -X --username=freecodecamp --dbname=students --no-align --tuples-only -c"`

## Paso 6
Agregar una query que se imprima en la terminal.
   `echo "$($PSQL "SELECT first_name, last_name, gpa FROM students WHERE gpa = 4.0;")"`

## Paso 7
Agregar un echo que imprima un comentario en la terminal.
   `echo -e "\nAll course names whose first letter is before 'D' in the alphabet:"`

## Paso 8
Agregar un echo para visualizar la columna course de la tabla courses donde sólo mostrará los valores alfabéticamente menores a la
    letra ‘D’.
   `echo "$($PSQL "SELECT course FROM courses WHERE course < 'D'")"`

## Paso 9
Agregar un enunciado que se imprima en la consola.
   `echo -e "\n\nFirst name, last name, and GPA of students whose last name begins with an 'R' or after and have a GPA greater than 3.8 or less than 2.0:"`

## Paso 10
Utilizamos el comando echo para imprimir en la consola el resultado de los estudiantes que cumplen con estas condiciones.
   `echo "$($PSQL "SELECT first_name, last_name, gpa FROM students WHERE last_name >= 'R' AND (gpa > 3.8 OR gpa < 2.0)")"`

## Paso 11
Agregar un enunciado que se imprima en la consola.
   `echo -e "\nLast name of students whose last name contains a case insensitive 'sa' or have an 'r' as the second to last letter:"`

## Paso 12
Utilizando el comando, un script que imprima los apellidos que contenga ‘sa’ y que la penúltima letra sea una ‘r’.
   `echo "$($PSQL "SELECT last_name FROM students WHERE last_name ILIKE '%sa%' OR last_name LIKE '%r_'")"`

## Paso 13
Agregar un enunciado que se imprima en la consola.
   `echo -e "\nFirst name, last name, and GPA of students who have not selected a major and either their first name begins with 'D' or they have a GPA greater than 3.0:"`

## Paso 14
Agrega un echo para visualizar a los estudiantes que no han seleccionado una carrera y además que su curso tiene una ‘D’ al inicio o su gpa es mayor a 3.0.
   `echo "$($PSQL "SELECT first_name, last_name, gpa FROM students WHERE major_id IS NULL AND (first_name LIKE 'D%' OR gpa > 3.0)")"`

## Paso 15
Agregar un echo que imprima los nombres de los primeros 5 cursos ordenados en reversa alfabéticamente y que su segunda letra sea ‘e’ o la última sea ’s’.
   `echo "$($PSQL "SELECT course FROM courses WHERE course LIKE '_e%' OR course LIKE '%s' ORDER BY course DESC LIMIT 5")"`

## Paso 16
Agrega un nuevo comentario.
   `echo -e "\nAverage GPA of all students rounded to two decimal places:"`

## Paso 17
Agrega un echo a la instrucción anterior donde devuelve el promedio del gpa de la tabla students con dos decimales después del punto.
   `echo -e "$($PSQL " SELECT ROUND(AVG(gpa), 2) FROM students")"`

## Paso 18
Agrega otro comentario con el comando echo.
   `echo -e "\nMajor ID, total number of students in a column named 'number_of_students', and average GPA rounded to two decimal places in a column name 'average_gpa', for each major ID in the students table having a student count greater than 1:"`

## Paso 19
Agregar un echo que muestre major_id, el número de estudiantes renombrado como number_od_students, el promedio de gpa redondeo con dos decimales después del punto renombrado como average_gpa. Todo lo agrupamos por el major_id y agregamos una última condición donde se muestren sólo quieren tienen más de un estudiante.
   `echo -e "$($PSQL " SELECT major_id, COUNT(*) as number_of_students, ROUND(AVG(gpa), 2) as average_gpa FROM students GROUP BY major_id HAVING COUNT(*) > 1")"`

## Paso 20
Agrega un nuevo comando echo para un comentario:
   `echo -e "\nList of majors, in alphabetical order, that either no student is taking or has a student whose first name contains a case insensitive 'ma':"`

## Paso 21
Agrega un echo script que devuelve los majors que no tienen estudiantes inscritos y también los estudiantes tienen ‘ri’ en su nombre:
   `echo "$($PSQL "SELECT major FROM students FULL JOIN majors ON students.major_id = majors.major_id WHERE major IS NOT NULL AND (student_id IS NULL OR first_name ILIKE '%ma%') ORDER BY major")"`

## Paso 22
Agrega un echo con un query.
   `echo "$($PSQL "SELECT DISTINCT(course) FROM students RIGHT JOIN majors USING(major_id) INNER JOIN majors_courses USING(major_id) INNER JOIN courses USING(course_id) WHERE (first_name = 'Obie' AND last_name = 'Hilpert') OR student_id IS NULL ORDER BY course DESC")"`

## Paso 23
Agrega comentario.
   `echo -e "\nList of courses, in alphabetical order, with only one student enrolled:"`

## Paso 24
Agrega un echo más.
   `echo "$($PSQL "SELECT course FROM students INNER JOIN majors_courses USING(major_id) INNER JOIN courses USING(course_id) GROUP BY course HAVING COUNT(student_id) = 1 ORDER BY course")"`

```
