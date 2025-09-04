# Laboratorio-1
Unidades Booteables y Sistemas Operativos 
# Proceso de Booteo y Conceptos Relacionados

Este documento explica el proceso de booteo en memorias USB creadas con **Rufus** y **Ventoy**, además de conceptos clave como el **bootloader**, **GRUB**, los **sistemas de archivos compatibles** y la **estructura de particiones**.

---

## 1. Proceso de Booteo en Rufus y Ventoy

- **Rufus**  
  - Rufus prepara la memoria USB creando una partición con un sistema de archivos (FAT32, NTFS, exFAT, etc.) y copiando los archivos de instalación de un sistema operativo.  
  - Además, escribe en el USB un **bootloader** que permite que la computadora arranque desde la memoria en lugar del disco duro.  
  - Con Rufus, la memoria se configura para un sistema específico (ejemplo: Windows o Linux). Si se quiere instalar otro ISO, se debe formatear y volver a crear.

- **Ventoy**  
  - Ventoy funciona de forma diferente: al instalarse en la memoria USB, crea una partición propia con un **bootloader (GRUB modificado)**.  
  - El usuario solo debe copiar los archivos ISO directamente al USB (sin necesidad de formatear cada vez).  
  - Al arrancar desde la memoria, Ventoy muestra un menú con todos los ISOs copiados, permitiendo elegir cuál iniciar.  
  - Esto lo hace más flexible y práctico para quienes usan varios sistemas operativos.

---

## 2. Bootloader y GRUB

- **Bootloader**  
  - Es un programa pequeño ubicado en la memoria booteable.  
  - Su función es iniciar el proceso de carga del sistema operativo, indicando a la computadora dónde se encuentran los archivos necesarios para arrancar.  
  - Sin un bootloader, la máquina no sabría cómo pasar del encendido a cargar un sistema operativo.

- **GRUB (GRand Unified Bootloader)**  
  - Es uno de los bootloaders más usados, especialmente en sistemas Linux.  
  - Permite elegir entre varios sistemas operativos o configuraciones en el arranque.  
  - Ventoy, por ejemplo, utiliza una versión modificada de GRUB para mostrar el menú de selección de ISOs.

---

## 3. Sistemas de Archivos Compatibles

Un **sistema de archivos** define cómo se organizan y almacenan los datos dentro de una partición. Los más comunes son:

- **FAT32**: Muy compatible con casi todos los sistemas y BIOS/UEFI, pero con límite de archivos de 4 GB.  
- **exFAT**: Evolución de FAT32, sin el límite de 4 GB.  
- **NTFS**: Sistema de archivos de Windows, soporta archivos grandes y permisos avanzados.  
- **ext4**: Usado en Linux, soporta grandes volúmenes y es muy estable.  

Cada herramienta (Rufus/Ventoy) selecciona el más adecuado según el sistema operativo que se quiera instalar.

---

## 4. Estructura de Particiones

Una **partición** es una división lógica dentro de un dispositivo de almacenamiento (ejemplo: un disco duro o USB).  
Permite que un mismo dispositivo se divida en secciones independientes.

### Tipos de particiones:

- **MBR (Master Boot Record)**  
  - Esquema más antiguo.  
  - Soporta discos hasta 2 TB y máximo 4 particiones primarias.  
  - Compatible con BIOS.

- **GPT (GUID Partition Table)**  
  - Esquema más moderno.  
  - Soporta discos mucho más grandes (hasta 9.4 ZB).  
  - Permite hasta 128 particiones.  
  - Compatible con UEFI.  

---

## 📌 Conclusión

- Rufus crea una memoria booteable para un sistema operativo específico.  
- Ventoy usa un bootloader (basado en GRUB) que permite iniciar múltiples ISOs desde una sola memoria.  
- El bootloader es esencial para que la computadora sepa cómo arrancar.  
- GRUB es uno de los bootloaders más usados en Linux y base del funcionamiento de Ventoy.  
- Los sistemas de archivos (FAT32, NTFS, exFAT, ext4) organizan los datos en la memoria.  
- La estructura de particiones (MBR o GPT) define cómo se divide y gestiona el espacio de almacenamiento.  

---
