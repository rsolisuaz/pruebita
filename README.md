# PRÁCTICA 5. CREACIÓN Y MANIPULACIÓN DE BASES DE DATOS EN MYSQL USANDO EL LENGUAJE SQL.

## COPIA DEL REPOSITORIO REMOTO EN SU COMPUTADORA LOCAL
Como primer paso, será necesario crear una copia local del repositorio remoto creado en Github al aceptar la tarea. Para ello, es necesario hacer los siguientes pasos:
1)	Entrar a la página cuyo URL les fue proporcionado al aceptar la tarea, en tal página dé click en el botón Code y copie el URL que aparece en el cuadro de texto de nombre **Clone with HTTPS** (comienza con *https://*)
2)	En una consola de Git Bash en Windows (o en una terminal en Linux o Mac), cree una carpeta donde quiera que se contengan sus prácticas del semestre (si es que aún no la has creado) y colócate en tal carpeta. La carpeta la puedes crear desde el Git Bash o terminal Linux/Mac usando el comando `mkdir` (o con el explorador de archivos de su sistema operativo) y en la consola de Git Bash o terminal de Linux/Mac te puedes cambiar a la carpeta mencionada usando el comando `cd`
3)	Clone el repositorio privado dando el comando `git clone URL practica05`
 (donde **URL** es el URL que copió en el paso 1)\
 Este comando creará dentro de la carpeta creada en el paso 2) una subcarpeta de nombre **practica05** donde estará una copia local del repositorio remoto.\
 Los comandos posteriores de git tendrán que darse desde tal carpeta, por tanto, cámbiate a la carpeta usando `cd practica05`


## REQUERIMIENTOS

En esta práctica, generará un par de scripts (archivos con comandos SQL) que contendrán una serie de sentencias SQL (terminadas con **;**) para crear un usuario y otorgarle permisos sobre la base de datos controlescolar_ej2021, crear 3 tablas en MySQL en tal base de datos, y colocar información en tales tablas. La base de datos representará parte de la información necesaria para llevar el control de las cargas de materias llevadas por un estudiante y/o impartidas por un profesor. 

1. Para efectos de poder probar en su computadora local los comandos incluidos en los scripts a realizar, deberá primero crear la base de datos con el comando siguiente:
`CREATE DATABASE IF NOT EXISTS controlescolar_ej2021;`

Este comando lo dará directamente en la consola de MySQL y no será incluido en los dos archivos que deberá crear en esta práctica.

2. Las sentencias SQL deberán ser colocadas en dos archivos de texto con extensión .sql y nombrados exactamente de la siguiente manera (todos los caracteres del nombre en minúsculas):  **tablas.sql** y **datos.sql**

3. El primer archivo (**tablas.sql**) deberá cumplir con lo siguiente:
   - Se colocarán al inicio los siguientes cinco comandos (donde XXXXXXXX se sustituye por su matrícula)
     ```
     USE controlescolar_ej2021;
	 DROP USER IF EXISTS 'U_XXXXXXXX'@'localhost';
	 DROP TABLE IF EXISTS carrera_XXXXXX;
	 DROP TABLE IF EXISTS materia_XXXXXX; 
	 DROP TABLE IF EXISTS profesor_XXXXXX;
     ``` 
   - Posteriormente deberá tener 2 comandos:
     - Un comando para crear el usuario U_XXXXXXXX (el cual se conectará desde localhost y con clave UAZsw$021)
     - Otro comando para otorgarle al usuario recién creado todos los permisos de acceso en la base de datos controlescolar_ej2021
   - Vendrá después un conjunto de sentencias para crear 3 tablas. Las tablas por crear serán algunas de las que se muestran en la siguiente figura (con la aclaración que a los nombres de las tablas que se muestran en la figura le tendrá que agregar `_XXXXXXXX` (donde XXXXXXXX es su matrícula):

   ![Diagrama Entidad-Relación de Base de Datos controlescolar](https://github.com/rsolisuaz/act03_desappint_ej2021/blob/master/imagenes/imagenactividad03.png)
     - Aspectos importantes a notar sobre la figura:
       - Que un campo tenga una llave amarilla a la izquierda indica que es la llave primaria
       - Que tenga un rombo con relleno rojo a la izquierda indica que es una llave foránea, es decir, que su valor es la llave primaria en alguna otra tabla (**PERO NO NECESITAN INDICAR EN SU SCRIPT QUE ES DE HECHO UNA LLAVE FORÁNEA**)
       - Que un campo tenga un rombo con relleno azul a la izquierda indica que debe dársele valor al momento de insertar un registro, es decir, su valor NO puede ser NULL. Se indica para cada campo el tipo de datos correspondiente. Las **tres** tablas a crear son las siguientes: `carrera_XXXXXXXX`,  `materia_XXXXXXXX` y `profesor_XXXXXX`
       - Recuerde sustituir las XXXXXXXX por su matrícula en el nombre de las tablas a crear
       - Recuerde que los campos con rombo relleno indican que no pueden ser NULL, por lo cual se les debe poner **NOT NULL** como atributo en la definición de la columna correspondiente
       - La tabla `materia_XXXXXX` contendrá los siguientes campos  y tipos: 
         - `clave_materia`  de tipo CHAR(10)
         - `nombre_materia` de tipo VARCHAR(50)
         - `semestre` de tipo TINYINT UNSIGNED
         - `clave_carrera`  de tipo CHAR(10) 
         - La llave primaria será el campo `clave_materia`. Todos los campos deben tener un valor al agregar un registro, es decir, tendrán la característica **NOT NULL**.
       - La tabla `profesor_XXXXXX` contendrá los siguientes campos  y tipos:
         - `rfc` de tipo CHAR(13)
         - `nombre` de tipo VARCHAR(25)
         - `ap_paterno` de tipo VARCHAR(20)
         - `ap_materno` de tipo VARCHAR(20)
         - `calle` de tipo VARCHAR(30)
         - `colonia` de tipo VARCHAR(30)
         - `cod_postal` de tipo CHAR(5)
         - `telefono`  de tipo CHAR(10)
         - `email`  de tipo VARCHAR(30)
         - `id_estado` de tipo SMALLINT
         - `id_municipio` de tipo INT
         - La llave primaria será el campo `rfc`. Los campos `rfc`, `nombre`, `ap_paterno` y `email` deben tener un valor al agregar un registro, es decir, tendrán la característica **NOT NULL**.
       - La tabla `carrera_XXXXXX` contendrá los siguientes campos  y tipos:
         - `clave_carrera` de tipo CHAR(10)
         - `nombre_carrera` de tipo VARCHAR(50)
         - La llave primaria será el campo `clave_carrera`. Todos los campos deben tener un valor al agregar un registro, es decir, tendrán la característica **NOT NULL**.
   - Después de los comandos para crear las tres tablas ponga los siguientes comandos al final del archivo **tablas.sql** (recuerde sustituir los XXXXXXXX por su matricula):
   ```
	SHOW TABLES LIKE '%XXXXXXXX';
	SELECT user,host FROM mysql.user;
   ```


La lista de requerimientos que deben cumplirse en esta práctica los puede encontrar en el archivo **PracticasLaboratorio05_24Sep2020.pdf**


## CALIFICACIÓN
La calificación para esta práctica no les será emitida de manera inmediata al subir su solución, sin embargo se realizarán pruebas para verificar que se pueden ejecutar los scripts SQL tablas.sql y datos.sql sin problemas en MySQL al hacer push de su practica.

**SI SUS SCRIPTS NO PUEDEN SER EJECUTADOS SIN ERRORES OBTENDRÁN CERO PUNTOS**


## NOTAS IMPORTANTES


1. Recuerda que de acuerdo a lo visto en las Prácticas Anteriores el proceso que debes estar haciendo es:
   - Haz cambios  en los archivos **tablas.sql** y **datos.sql**
   - **Verifica que funcionan correctamente ejecutándolos en la consola de MySQL usando SOURCE** (trata de ir haciendo cambios incrementales, por ejemplo, agrega algunas de las sentencias SQL que debe tener uno de los archivos, y prueba que funcione antes de agregar mas sentencias SQL)
   - Para avisar a tu repositorio local que registre los cambios emite los comandos `git add NNNNN.sql` (donde NNNNN es el nombre del archivo que modificaste) y `git commit -m "MENSAJE"` donde MENSAJE es un texto que describe brevemente, pero de manera clara los cambios que realizaste desde el último commit.

2. Después de haber hecho todos los commits que completan tus scripts, súbelos al repositorio remoto dando `git push`

3. Cada vez que hagas `git push` se realizarán automáticamente pruebas sobre tu código para verificar si pueden ser ejecutados sin errores en MySQL. Para esta práctica en particular no se te proporcionará una calificación de manera inmediata pues debe ser revisada con mayor detalle. Recuerda que en la página de tu repositorio en la sección **Pull Requests**, se encuentra una subsección de nombre **Feedback**, donde podrás encontrar los resultados de las pruebas en la pestaña denominada **Check** (expandiendo la parte que dice **Run education/autograding@v1**), y cualquier comentario general que el profesor tenga sobre tu código en la pestaña **Conversation**. 
