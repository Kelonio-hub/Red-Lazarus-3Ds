# Red-Lazarus-3Ds

1. Introducción:

Red Lazarus es un Script .gm9 que revive consolas de la marca Nintendo 3ds y 2ds (tanto modelo Old como New). 
Su estrutura parte del script Lazarus de AnalogMan151, con la gran diferencia de que este proceso PERMITE ELIMINAR EL CFW SIN PROVOCAR UN NUEVO BRICK.  
No obstante, el proceso no instala el Movable ni de las APP Universales, teniendo que realizar a futuro el proceso de CTRTransfer genérico. 


2. Créditos:
- Angelpro09_xd, quien descubió la falla al quitar por error la SD en el proceso Lazarus.
- Kelonio 3Ds, por reestructurar el script y darlo a conocer. 
- Yakara Colombia, por los archivos donantes usuados durante las pruebas.


3. Objetos físicos:
- Consola con brick azul 
- R4 flasheada


4. Archivos en SD: 
- Archivo de ntrboot para conectar a la R4
- Archivo boot.firm de Luma o Godmode9 en sd/
- Archivo Godmode9.firm en sd/luma/payloads
- Archivo Red Lazarus.gm9 en sd/gm9/scripts
- Carpeta Lazarus en sd/

Archivos dentro de la ruta sd/Lazarus: 
- nand_hdr.bin
- sighax_hdr_retail.bin
- twlmbr.bin
- twln.bin
- twlp.bin
- ctrtransfer_^.bin ^(o3ds/o2ds/n3ds/n2ds)^

5. Proceso del Script

################# Proceso Red Lazarus #################

ask "Este Script revive sin Lazarus Permanente\nContinuar?"
set ERRORMSG "Cancelado por el usuario."


set ERRORMSG "Cancelado por el usuario."
allow -a S:


################# Comprobando Archivos ################# 

set ERRORMSG "ARCHIVOS NECESARIOS NO ENCONTRADOS. \n \nVUELVE A DESCARGAR O USA OTRA TARJETA SD "

find 0:/Lazarus/NAND_hdr.bin HDR

find 0:/Lazarus/sighax_hdr_*.bin SIGHAX

find 0:/Lazarus/twlmbr.bin TWLMBR

find 0:/Lazarus/twln.bin TWLN

find 0:/Lazarus/twlp.bin TWLP

find 0:/Lazarus/ctrtransfer_o2ds.bin CTRNAND


################# Restaurando NAND, TWL y Fixeando rutas ################# 

set ERRORMSG "ERROR EN LA RESTAURACION. \n \nVUELVE A DESCARGAR O USA OTRA TARJETA SD"

cp -w -n $[HDR] S:/nand.bin

cp -w -n $[SIGHAX] S:/nand_hdr.bin

cp -w -n $[TWLMBR] S:/twlmbr.bin

cp -w -n $[TWLN] S:/twln.bin

cp -w -n $[TWLP] S:/twlp.bin

cp -w -n $[CTRNAND] S:/ctrnand_full.bin

fixcmac 1:/dbs

fixcmac 1:/data

fixcmac 1:/private

echo "Consola Revivida con Red Lazarus. #TeAmoKelonio"

reboot
