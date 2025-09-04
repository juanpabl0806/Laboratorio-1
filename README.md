# Laboratorio 1: Unidades Booteables y Sistemas Operativos 

# Proceso de Booteo y Conceptos Relacionados

Este documento explica el proceso de booteo en memorias USB creadas con **Rufus** y **Ventoy**, además de conceptos clave como el **bootloader**, **GRUB**, los **sistemas de archivos compatibles** y la **estructura de particiones** incluyendo sus respectivos procedimientos para la correcta instalacion .

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

# Instalación de Ubuntu usando una USB booteable (Rufus o Ventoy)

> **Recomendación:** Haz copia de seguridad antes de modificar particiones. Conecta el cargador si es un portátil.

---

## 0) Requisitos

* USB de **8 GB** o más.
* Imagen **ISO de Ubuntu** (ej. Ubuntu 24.04 LTS).
* **Rufus** (Ubuntu) o **Ventoy** (Windows/Linux).
* PC con **UEFI/BIOS** y acceso al menú de arranque (teclas típicas: **F2**, **F9**, **Esc**, **F10**, **F11** según fabricante).

---

## 1) Crear la USB booteable

* Si quieres tener varios sistemas en la misma USB:

     - Usa Ventoy → solo se instala una vez en la USB, y luego solo copias las ISOs dentro de la memoria.

      - Al arrancar, puedes elegir qué sistema iniciar.

---

## 2) Arrancar el PC desde la USB

1. Con la USB conectada, **reinicia** y abre el **menú de arranque** (F12/F9/Esc… según tu equipo).
2. Selecciona **UEFI: <Tu USB>** si tu firmware es UEFI (recomendado). Si no, selecciona la USB en modo Legacy/BIOS.
3. Con **Rufus** verás directamente el instalador de Ubuntu.
   Con **Ventoy** verás un **menú**: elige la **ISO de Ubuntu**.

**Pantallazos (inserta aquí):**

 
* <img width="400" height="500" alt="image" src="https://github.com/user-attachments/assets/154a6735-e6ae-4a3c-bc95-170ecc42237a" />
*<img width="400" height="600" alt="image" src="https://github.com/user-attachments/assets/cd17842d-5222-46d3-9245-e2ef038839f3" />
*<img width="400" height="532"   alt="image" src="https://github.com/user-attachments/assets/b7c26ed8-06c4-4d3e-8e9d-f2a612374cf2" />



> Si recibes errores con *Secure Boot*, puedes **desactivarlo** temporalmente en BIOS/UEFI o, en Ventoy, **enrolar la clave** si el fabricante lo permite.

---

## 3) Instalación de Ubuntu: paso a paso

> A continuación se muestra la ruta **guiada** con creación de particiones. Si ya hiciste espacio desde Windows (Administración de discos), salta directo a **3.5 Particionado manual (Something Else)**.

### 3.1 Idioma e inicio

* En **GNU GRUB version**, elige **Try or Install Ubuntu**
 <img width="400" height="502" alt="image" src="https://github.com/user-attachments/assets/b2283610-0203-4ef0-9e1d-e8beba22968b" />


* Elige **Español** y pulsa **Instalar Ubuntu**.

*<img width="400" height="500" alt="image" src="https://github.com/user-attachments/assets/9480ebe8-5312-43ba-897c-425a0b829374" />


*<img width="400" height="500" alt="image" src="https://github.com/user-attachments/assets/99a7df50-b27a-497a-8e77-91c779860596" />

### 3.2 Conexión de red

* Conéctate a Wi‑Fi o red cableada para descargar actualizaciones/controladores durante la instalación (opcional pero recomendado).


### 3.3 Tipo de instalación

* **Instalación normal** (con utilidades y navegador) o **mínima** (más ligera).
* Marca **Descargar actualizaciones** y **Software de terceros** si quieres controladores propietarios (gráfica/Wi‑Fi) desde el inicio.

**Pantallazo:**

* <img width="400" height="550" alt="image" src="https://github.com/user-attachments/assets/b2945a0f-c55f-4aa9-894a-b2c7623ebaa3" />

### 3.4 Método de particionado

* Si aparece la opción **“Instalar Ubuntu junto a…”**, puedes usarla para redimensionar automáticamente.
* Para control total, elige **“Más opciones / Something else”**. Aquí crearemos las particiones manualmente.

**Pantallazo:**

* <img width="400" height="506" alt="image" src="https://github.com/user-attachments/assets/ff50adee-4108-4bf1-8bd3-ddad160c7ca1" />


### 3.5 Particionado manual (Something Else)

Primero, identifica si tu disco usa **GPT/UEFI** (lo usual en equipos modernos) o **MBR/BIOS**.

#### 3.5.1 Esquema recomendado en UEFI (GPT)

* **ESP (EFI System Partition)**: suele existir ya (100–500 MB, **FAT32**).

  * **Acción**: selecciónala, marca **punto de montaje /boot/efi** y **NO formatear**.
* **/ (raíz)**: **ext4**, **30–50 GB** (o más si podrás instalar muchas apps).
* **swap**: 2–8 GB (si tienes mucha RAM, 2–4 GB suele bastar).

#### 3.5.2 Esquema recomendado en BIOS/Legacy (MBR)

* **/ (raíz)**: **ext4**, 30–50 GB o más.
* **swap**: 2–8 GB.
* (Opcional) **/home**: ext4 con el resto del espacio.

>
> * En **UEFI/GPT** suele ser el **disco** (ej. */dev/nvme0n1*) y el instalador pondrá GRUB en la **ESP**.
> * En **MBR/BIOS** también elige el **disco** principal (no una partición).


### 3.6 Confirmación de cambios

* Acepta los cambios de particionado cuando el instalador te lo pida (esto **escribe en disco**).

**Pantallazo:**

* <img width="406" height="510" alt="image" src="https://github.com/user-attachments/assets/f3058f43-f626-4d06-a91d-bf5aa644fa3e" />


### 3.7 Zona horaria

* Selecciona tu ciudad/región.

**Pantallazo:**

* <img width="400" height="506" alt="image" src="https://github.com/user-attachments/assets/2755862b-3a06-4e14-ba3c-69ea69d4ba12" />
* <img width="407" height="506" alt="image" src="https://github.com/user-attachments/assets/cc25fccf-8342-433e-b533-a27c0c1c819f" />

* <img width="400" height="577" alt="image" src="https://github.com/user-attachments/assets/224e6db6-c4b3-48d1-964d-0139de2107ef" />


### 3.8 Usuario y contraseña

* Crea tu usuario, nombre del equipo y contraseña. Puedes elegir **iniciar sesión automáticamente** o pedir contraseña.

**Pantallazo:**

* <img width="400" height="516" alt="image" src="https://github.com/user-attachments/assets/a566906b-19f4-4368-ad21-0bb3095965c6" />


### 3.9 Instalación y reinicio

* Espera a que finalice la copia de archivos y la configuración.
* Pulsa **Reiniciar ahora** y **retira la USB** cuando el sistema lo indique.

**Pantallazos (inserta aquí):**

* <img width="400" height="537" alt="image" src="https://github.com/user-attachments/assets/8ebd4537-0404-42a2-8028-b5da35561b62" />


---

## 4) Primer arranque y verificación (dual-boot)

1. Si también tienes Windows, al encender verás el **menú de GRUB** con Ubuntu y Windows.
2. Inicia en Ubuntu. Abre una terminal y ejecuta:

" sudo apt update && sudo apt upgrade -y "

---

## 5) Solución de problemas comunes

* **No aparece la USB en el menú de arranque:** prueba otro puerto, recrea la USB en **FAT32**, verifica que está en modo **UEFI** si tu firmware es UEFI.
* **Error con Secure Boot:** desactívalo temporalmente o usa la opción de **enrolar clave** (Ventoy). Ubuntu suele soportar Secure Boot.
* **Falta opción “Instalar junto a Windows”:** usa **Más opciones (Something Else)** y crea las particiones manualmente.
* **No veo la partición EFI (ESP):** en equipos UEFI debería existir (\~100–500 MB, FAT32). No la borres; selecciónala como **/boot/efi** sin formatear.

---

## 📌 Conclusión

- Rufus crea una memoria booteable para un sistema operativo específico.  
- Ventoy usa un bootloader (basado en GRUB) que permite iniciar múltiples ISOs desde una sola memoria.  
- El bootloader es esencial para que la computadora sepa cómo arrancar.  
- GRUB es uno de los bootloaders más usados en Linux y base del funcionamiento de Ventoy.  
- Los sistemas de archivos (FAT32, NTFS, exFAT, ext4) organizan los datos en la memoria.  
- La estructura de particiones (MBR o GPT) define cómo se divide y gestiona el espacio de almacenamiento.  

---
