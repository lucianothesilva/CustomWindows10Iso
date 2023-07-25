[![pt-br](https://img.shields.io/badge/lang-pt--br-green.svg)](https://github.com/lucianothesilva/CustomWindows10Iso/blob/main/README.pt-br.md)
[![en](https://img.shields.io/badge/lang-en-red.svg)](https://github.com/lucianothesilva/CustomWindows10Iso/blob/main/README.md)

**Cómo crear una ISO personalizada de Windows 10 con software preinstalado.**

Software necesario:

**Windows ADK para Windows 10 (Herramientas de implementación):** Asegúrate de descargar la versión correcta de Windows ADK para tu versión de Windows 10 (por ejemplo, Windows 10 versión 1909, 20H2, etc.)
   - [Descargar Windows ADK](https://developer.microsoft.com/en-us/windows/hardware/windows-assessment-deployment-kit)

**Rufus (Para crear una unidad USB booteable):**
   - [Descargar Rufus](https://rufus.ie/)

1. **Formatear una máquina e instalar el software:**
   - Formatea la máquina y crea una cuenta local con el nombre deseado.
   - Instala los programas necesarios y elimina el bloatware (aplicaciones innecesarias).

2. **Ejecutar la Limpieza de Disco:**
   - Abre la Limpieza de Disco (Busca "Limpieza de Disco" en el menú de Inicio).
   - Selecciona los archivos del sistema que deseas eliminar y procede.

3. **Reducir el tamaño de la unidad C:\ y crear una nueva partición:**
   - Presiona la tecla Windows + X y selecciona "Administración de discos".
   - Haz clic derecho en la unidad C:\ (generalmente etiquetada como "OS (C:)") y elige "Reducir volumen".
   - Ingresa el tamaño deseado para reducir la partición y crea un espacio sin asignar.
   - Haz clic derecho en el espacio sin asignar y selecciona "Nuevo volumen simple".
   - Asigna la letra de unidad "D" y etiquétala como "Image".

4. **Crear carpetas en la unidad D:\:**
   - Abre el Explorador de archivos (Win + E) y navega hasta la unidad D:\.
   - Haz clic derecho en un área vacía y selecciona "Nuevo" > "Carpeta".
   - Nombra la carpeta como "Scratch".
   - Crea otra carpeta llamada "iso_files".

5. **Apagar la máquina:**
   - Guarda tu trabajo y cierra todas las aplicaciones.
   - Haz clic en Inicio > Apagar.

6. **Arrancar desde la unidad USB de Windows y abrir el símbolo del sistema:**
   - Inserta la unidad USB de Windows y reinicia la máquina.
   - Accede a la BIOS o al menú de arranque (generalmente F2, F12, Esc o Del) durante el inicio.
   - Selecciona la unidad USB como dispositivo de arranque.
   - En la pantalla de configuración de Windows, presiona Shift + F10 para abrir el símbolo del sistema.

7. **Capturar la imagen en formato .wim:**
   - En el símbolo del sistema, ejecuta el siguiente comando:
     ```
     dism /capture-image /imagefile:D:\install.wim /capturedir:C:\ /ScratchDir:D:\Scratch /name:Windows10 /compress:maximum /checkintegrity /verify /bootable
     ```

8. **Montar la ISO de Windows y copiar el contenido:**
   - Monta una ISO de Windows (que coincida con la versión instalada) en tu máquina.
   - Copia el archivo "Windows10.wim" desde la ISO montada a "D:\iso_files\Sources" y reemplaza el archivo existente.

9. **Descargar e instalar Windows ADK:**
   - Descarga Windows ADK para Windows 10 [desde el sitio web de Microsoft](https://developer.microsoft.com/en-us/windows/hardware/windows-assessment-deployment-kit), si aún no lo has hecho.

10. **Ejecutar las Herramientas de Implementación como Administrador:**
    - Ejecuta "Entorno de herramientas de implementación e imágenes" como administrador.

11. **Crear la ISO personalizada:**
    - En el símbolo del sistema abierto, ejecuta el siguiente comando:
      ```
      oscdimg.exe -m -o -u2 -udfver102 -bootdata:2#p0,e,bd:\iso_files\boot\etfsboot.com#pEF,e,bd:\iso_files\efi\microsoft\boot\efisys.bin d:\iso_files d:\Windows10Inside.iso
      ```

12. **Usar Rufus para crear una unidad USB booteable:**
    - Usa la herramienta Rufus para crear una unidad USB booteable utilizando la ISO personalizada.

13. **¡Utiliza la unidad USB booteable en tus máquinas
