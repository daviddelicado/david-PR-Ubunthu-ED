**Instrucciones tarea1:**

1. **Consulta el Archivo de Referencia:**
   - El alumnado deberá consultar el archivo *Manual_de_comandos_ubunthu.pdf*.

2. **Identifica la Combinación de Cifras:**
   - Según la fecha de nacimiento de cada estudiante, identificarán una combinación específica de cifras.

3. **Modificación del Archivo "1.md":**
   - En el archivo PDF, cada cifra corresponde a un punto específico. Por ejemplo, si la combinación es "14", deberás añadir al archivo *1.md* los puntos correspondientes a "1" y "4" desde el archivo PDF.

4. **Evaluación de Habilidades:**
   - Esta tarea evaluará la habilidad de los estudiantes para clonar un repositorio a través de fork en GitHub, así como para crear y modificar archivos.

# HE NACIDO EL 18/06 

1. INTRODUCCIÓN
Un intérprete de comandos es un programa que toma la entrada del usuario, por ejemplo las órdenes que
teclea, y la traduce a instrucciones. Podemos compararlo con el COMMAND.COM de MS-DOS.

En cualquier GNU/Linux tenemos la llamada terminal o consola que abre un shell o intérprete de
comandos. En Ubuntu la abrimos buscando en en el Dash o tablero de Unity: "Terminal" o pulsando la
combinación de teclas Ctrl + Alt + T

También se puede pasar al modo texto (intérprete de comandos) desde el modo gráfico
pulsando: Ctrl + Alt + F1 o bien con: F2 F3 F4 F5 F6 .
Esto hace que el sistema salga del modo gráfico y acceda a alguna de las seis consolas virtuales de Linux, a
las cuales también se puede acceder cuando se arranca en modo de texto.
Para volver al modo gráfico hay que presionar Ctrl + Alt + F7 o Ctrl + Alt + F8 (Según la sesión en modo
gráfico a la que deseemos regresar).
Enlaces de interés:
GNU Emacs, Manuales Online
Una introducción rápida a GNU Emacs

8. OTROS COMANDOS BÁSICOS

du y df → (Espacio ocupado en el disco)
El comando du permite conocer el espacio ocupado en el disco por un determinado directorio y todos los
subdirectorios que cuelgan de él. Para usarlo basta simplemente colocarse en el directorio adecuado y
ejecutar:
du
Este comando da el espacio de disco utilizado en bloques. Para obtener la información en bytes se debe
emplear el comando con la opción "-h":
du -h
El comando df por el contrario informa del espacio usado por las particiones del sistema que se encuentren
montadas:
df
Como el anterior, da el espacio en bloques. Para obtener la información en bytes se debe emplear el comando
con la opción "-h":
df -h

lpr → (Impresión)
Se emplea para imprimir una serie de ficheros. Si se emplea sin argumentos imprime el texto que se
introduzca a continuación en la impresora por defecto. Por el contrario ...
lpr nombre_fichero
... imprime en la impresora por defecto el fichero indicado.

ln → (Enlaces a ficheros)
Los enlaces nos van a permitir realizar copias de los ficheros (archivos o carpetas) con otro nombre, para
poder acceder a ellos desde lugares distintos a su ubicación original, con un ahorro de espacio muy importante
con respecto al comando cp.
Nuestro sistema identifica a los ficheros mediante un número denominado inodo, que les asigna en el
momento de su creación. Es decir, un directorio lo que contiene realmente es una lista de números de inodo
con sus correspondientes nombres de fichero. De esta forma, cada nombre de fichero es un enlace a un inodo
particular; por ello, cada inodo está asociado a un conjunto de información guardada en el disco, que puede
tener asignados distintos nombres, y a la que podremos acceder desde distintos lugares del árbol de directorios
si así lo deseamos.
En este sentido, podremos crear dos tipos distintos de enlaces a ficheros: enlaces duros y enlaces simbólicos.
El comando ln nos servirá para crear ambos tipos de enlaces. La sintaxis es la siguiente:
ln [opciones] origen [dest]ln [opciones] origen... directorio
ENLACES DUROS (HARD LINKS)
Si utilizamos el comando ln sin especificar ninguna opción, por defecto crearemos un enlace duro.
Obviamente, el fichero o ficheros para los que deseamos crear un enlace duro deberán existir. Así mismo, si el
último argumento es el nombre de un directorio que existe, crearemos un enlace duro a cada fichero, dentro
del directorio, y con el mismo nombre de fichero.
Si solamente especificamos el fichero que queremos enlazar, y no indicamos ningún nombre para el enlace,
éste se creará con el mismo nombre que el fichero a enlazar.
Los cambios que realicemos en el fichero enlazado o en el enlace, se reflejarán en el resto, ya que todos
tendrán el mismo número de inodo, y por lo tanto hacen referencia al mismo conjunto de información.
La ventaja de utilizar enlaces duros radica en que el comando "rm" únicamente borrará aquel fichero que le
indiquemos. La información solamente se borrará por completo cuando borremos todos los enlaces a un
inodo.
La desventaja con respecto a los enlaces simbólicos es que sólo permite crear enlaces dentro del mismo
sistema de ficheros.
Los directorios . y .. son enlaces duros al directorio actual y a su directorio padre respectivamente.
Ejemplo:
1 – Creamos el fichero pruebaln con la orden cat.
cat > pruebaln
Pulsamos Enter, escribimos algo, por ejemplo "hola" y pulsamos Enter y Ctrl + D para guardarlo.
2 – Creamos un enlace a pruebaln que se llame penlace.
ln pruebaln penlace
3 – Veamos las características de estos ficheros con la orden ls. Utilizamos la opción "-i" para ver el
número de inodo. Ambos tendrán el mismo número de inodo con dos enlaces.
kaos1310@kaos:~$ ls -i pruebaln penlace
2753739 penlace 2753739 pruebaln
4 – Ahora modificamos pruebaln añadiendo otra línea ...
cat >> pruebaln
Pulsamos Enter, escribimos algo, por ejemplo "adios", pulsamos Enter y Ctrl + D para guardarlo.
... y comprobamos si también se modifica penlace:
kaos1310@kaos:~$ cat pruebaln
hola
adios
kaos1310@kaos:~$ cat penlace
hola
adios5 – Ahora modificamos penlace añadiendo otra línea ...
cat >> penlace
Pulsamos Enter, escribimos algo, por ejemplo "otra vez hola", pulsamos Enter y Ctrl + D para guardarlo.
... y comprobamos si también se modifica pruebaln.
kaos1310@kaos:~$ cat penlace
hola
adios
otra vez hola
kaos1310@kaos:~$ cat pruebaln
hola
adios
otra vez hola
6 – Eliminamos pruebaln ...
rm pruebaln
... y comprobamos si penlace permanece y contiene la información correspondiente.
kaos1310@kaos:~$ cat penlace
hola
adios
otra vez hola
7 – Si utilizamos la orden ls -i, vemos que penlace sigue con el mismo número de inodo, que ahora
solamente tendrá un enlace:
kaos1310@kaos:~$ ls -i penlace
2753739 penlace
ENLACES SIMBÓLICOS
Si utilizamos la opción -s con el comando ln, es decir ln -s, crearemos un enlace simbólico. La sintaxis en
este caso es la misma que utilizamos para crear enlaces duros.
Podemos encontrar una similitud entre este tipo de enlaces y los accesos directos que estamos acostumbrados
a crear con los Win2.
En el caso de los enlaces simbólicos, cada fichero tendrá un número de inodo distinto. Sin embargo, al igual
que con los enlaces duros, todos los cambios que se realicen en uno de los ficheros se verán reflejados en el
resto.
Si borramos el fichero enlazado, el enlace simbólico perderá toda la información, puesto que su inodo apunta
a un número de inodo que ya no existe. Sin embargo, podremos crear enlaces simbólicos a ficheros de otros
sistemas de archivos.
Ejemplo:
1 – Aún tenemos el fichero penlace. Creamos un enlace duro a penlace que se llame pruebaln.
ln penlace pruebaln2 – Con la orden ls -li vemos que ambos tienen el mismo inodo, y que este inodo tiene dos enlaces.
kaos1310@kaos:~$ ls -li pruebaln penlace
2753739 -rw-r--r-- 2 kaos1310 kaos1310 25 dic 21 10:40 penlace
2753739 -rw-r--r-- 2 kaos1310 kaos1310 25 dic 21 10:40 pruebaln
3 – Creamos un enlace simbólico a penlace que se llame penlacesim.
ln -s penlace penlacesim
4 – Con la orden ls -li vemos que tienen distinto número de inodo. Además, el inodo de penlacesim sólo
tiene un enlace, y el inodo de penlace sigue teniendo dos. En la línea correspondiente a penlacesim vemos que
aparece el fichero al que apunta, y la letra "l" (ele) al inicio de los permisos.
kaos1310@kaos:~$ ls -li pruebaln penlace penlacesim
2753739 -rw-r--r-- 2 kaos1310 kaos1310 25 dic 21 10:40 penlace
2783398 lrwxrwxrwx 1 kaos1310 kaos1310 7 dic 21 11:00 penlacesim -> penlace
2753739 -rw-r--r-- 2 kaos1310 kaos1310 25 dic 21 10:40 pruebaln
5 – Cambiamos penlace y comprobamos si cambia penalcesim.
cat >> penlace
Pulsamos Enter, escribimos algo, por ejemplo "otra vez adios", pulsamos Enter y Ctrl + D para guardarlo.
kaos1310@kaos:~$ cat penlacesim
hola
adios
otra vez hola
otra vez adios
6 – Por último borramos penlace. Comprobamos que pruebaln permanece y que no podemos ver el contenido
de penlacesim, el sistema nos dirá que no existe. Para que desaparezca totalmente tenemos que borrarlo,
además borramos pruebaln para dejar todo como estaba sin las pruebas que hemos hecho.
rm penlace
kaos1310@kaos:~$ cat pruebaln
hola
adios
otra vez hola
otra vez adios
kaos1310@kaos:~$ cat penlacesim
cat: penlacesim: No existe el archivo o el directorio
rm penlacesim
rm pruebaln