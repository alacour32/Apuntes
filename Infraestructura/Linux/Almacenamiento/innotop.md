### Paso 1: Instalar las Dependencias Necesarias

Antes de instalar innotop, asegúrate de que tienes las herramientas necesarias instaladas. En Red Hat, esto generalmente implica instalar algunos paquetes de desarrollo de Perl y las utilidades de red.


`sudo dnf install perl-DBI perl-DBD-MySQL perl-TermReadKey ncurses-devel gcc make`

### Paso 2: Descargar e Instalar Innotop

Dado que innotop no siempre está disponible en los repositorios oficiales, puedes instalarlo desde su fuente directamente.

1. **Descargar Innotop:**
    
    Ve al [sitio oficial de innotop en GitHub](https://github.com/innotop/innotop) para descargar la última versión del código fuente. Puedes usar `wget` o `curl` para descargar el archivo de forma directa si tienes la URL del tarball.
    
    
    `wget https://github.com/innotop/innotop/archive/refs/tags/v1.11.7.tar.gz`
    
    (Nota: Asegúrate de usar la URL correcta para la última versión. La versión `1.11.7` es un ejemplo, verifica en GitHub la última).
    
2. **Extraer el Archivo Descargado:**
    
    Extrae el archivo tar descargado.
    
    `tar -xzf v1.11.7.tar.gz cd innotop-1.11.7`
    
3. **Instalar Innotop:**
    
    Ejecuta los siguientes comandos para construir e instalar innotop.
    
    `perl Makefile.PL make sudo make install`
    

### Paso 3: Verificar la Instalación

Una vez que la instalación esté completa, puedes verificar si innotop se ha instalado correctamente ejecutando:

`innotop --version`

### Paso 4: Usar Innotop

Para comenzar a usar innotop, simplemente ejecuta el comando:

`innotop`

Esto te llevará a la interfaz de innotop, donde puedes conectarte a tu servidor MySQL o MariaDB y comenzar a monitorear el rendimiento.

