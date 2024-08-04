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
`Touch nombre_del_archivo.sh` - Crear un nuevo archivo sh
`chmod +x nombre_de_archivo.sh` - Dar los permisos necesarios al archivo de ejecutar scripts.

# Tutorial 1

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
















   

```
