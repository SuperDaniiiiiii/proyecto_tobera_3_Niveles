================================================================================
ENTORNO DE SIMULACION CFD - OPENFOAM / BLUECFD
================================================================================

DESCRIPCION
-----------
Este repositorio contiene las carpetas, mallas y configuraciones necesarias para
ejecutar y analizar las simulaciones fluidodinamicas en OpenFOAM mediante el
entorno blueCFD-Core en Windows.


REQUISITOS PREVIOS
------------------
- blueCFD-Core instalado (OpenFOAM para Windows).
- ParaView (incluido dentro de la instalacion de blueCFD).


INSTRUCCIONES DE EJECUCION
--------------------------
1. Abrir la terminal de blueCFD:
   Busca "blueCFD-Core terminal" en el menu de inicio y ejecutala.

2. Navegar a la carpeta del caso:
   Usa el comando cd para entrar al directorio donde estan los archivos del
   caso que deseas simular (el que contiene las carpetas 0, constant y system).

   Ejemplo:
   $ cd /c/ruta/a/tu/repositorio/nombre_del_caso

3. Ejecutar la simulacion:
   Una vez dentro de la carpeta del caso, inicia el solucionador ejecutando:

   $ foamRun

   Espera a que el calculo termine y la terminal te devuelva el control. Si
   deseas guardar un registro de la ejecucion en un archivo de texto, usa:

   $ foamRun > log.run &
   $ tail -f log.run


VISUALIZACION DE RESULTADOS
---------------------------
Cuando la simulacion haya finalizado, tienes dos opciones para abrir los
resultados en ParaView:

Opcion A - Directo desde terminal (sin crear archivos extra):
   $ paraFoam

Opcion B - Creando un archivo puente para abrirlo manualmente en ParaView:
   $ touch caso.foam

   Despues abre el programa ParaView, ve a File -> Open y selecciona el
   archivo "caso.foam" que se acaba de crear dentro de la carpeta.


COMANDOS ADICIONALES UTILES
---------------------------
* Limpiar resultados anteriores (borra pasos de tiempo y mallas generadas):
  $ foamCleanTutorials

* Generar la malla base (si el caso usa blockMeshDict):
  $ blockMesh

* Refinar malla compleja (si el caso usa snappyHexMeshDict):
  $ snappyHexMesh -overwrite

* Verificar la calidad de la malla antes de correr:
  $ checkMesh

* Correr simulacion en paralelo (ejemplo con 4 nucleos):
  $ decomposePar
  $ mpirun -np 4 foamRun -parallel
  $ reconstructPar

* Detener una simulacion que esta corriendo en primer plano:
  Presiona Ctrl + C en la terminal.


ESTRUCTURA BASICA DE CADA CASO
------------------------------
/nombre_del_caso
  |-- 0/          (Condiciones iniciales y de frontera: U, p, T, etc.)
  |-- constant/   (Propiedades fisicas, turbulencia y archivos de malla)
  |-- system/     (Control de tiempo, esquemas numericos y solucionadores)
================================================================================
