# findCredentials (Windows - PowerShell | Linux - Bash)

********************************************************
*** Buscar credenciales en archivos de configuración ***
********************************************************

***Windows***

Busca archivos .config dentro de la unidad E:\ y luego busca la palabra "password" en su contenido.
  
    Get-ChildItem -Path "E:\" -Filter "*.config" -recurse | Select-String "password" | Select Filename, LineNumber, Line, Path | Format-List * | Out-File infoPassW.txt -append -width 5200

Que hace cada sentencia del comando:

  Buscar recursivamente (incluyendo subdirectorios) en la unidad E:\ todos los archivos con la extensión .config.
  
    Get-ChildItem -Path "E:\" -Filter "*.config" -Recurse

  Filtra el contenido de los archivos .config, buscando líneas que contengan la palabra "password".
  
    | Select-String "password"

  Selecciona y muestra la siguiente información de los resultados de la búsqueda:
  Filename: el nombre del archivo.
  LineNumber: el número de la línea donde se encontró la palabra "password".
  Line: la línea de texto completa donde se encontró la palabra.
  Path: la ruta completa del archivo.
  
    | Select Filename, LineNumber, Line, Path

  Da formato a la salida como una lista, donde cada propiedad se muestra en una nueva línea, en lugar de una tabla.
  
    | Format-List *

  Guarda la salida en un archivo de texto llamado infoPassW.txt.
  Usa -Append para añadir el contenido al archivo, en lugar de sobrescribirlo.
  Usa -Width 5200 para especificar un ancho de salida de 5200 caracteres por línea (evitando el truncado de líneas).
  
    | Out-File infoPassW.txt -Append -Width 5200



***Linux***

Este comando es para sistemas basados en Unix (como Linux o macOS) y realiza lo siguiente:

    find / -name '*.conf' -exec grep -Hn "password" {} \; >> infoPassL.txt

Que hace cada sentencia del comando:
  Busca de forma recursiva en todo el sistema (a partir de la raíz /) archivos con la extensión .conf.
  
    find / -name '*.conf'

  Por cada archivo encontrado, ejecuta el comando grep para buscar el texto "password" dentro del archivo. El modificador -Hn hace que grep muestre el nombre del archivo (-H) y el número de línea (-n) donde aparece la palabra "password".
  
    -exec grep -Hn "password" {} \;

  Los resultados se agregan (sin sobrescribir) al archivo infoPassL.txt.
  
    >> infoPassL.txt
