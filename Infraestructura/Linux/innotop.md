Para instalar **innotop** (un monitor avanzado de bases de datos MySQL/MariaDB), sigue estos pasos según tu sistema operativo:

---

### **1. Requisitos Previos**

- **Sistema operativo**: Linux (Ubuntu/Debian, RHEL/CentOS) o macOS.
    
- **Dependencias**:
    
    - Perl (`perl` >= 5.8).
        
    - Módulos Perl (`DBI`, `DBD::mysql`, `Term::ReadKey`, etc.).
        
    - Cliente MySQL/MariaDB (`mysql-client` o `mariadb-client`).

#### **2: Instalación manual**

- **Instala dependencias**
```bash 
sudo yum install mysql-devel perl perl-DBI perl-DBD-MySQL perl-TermReadKey git
```
- **Inapacion de dependencias por CPAN**
```bash
cpan DBD::mysql 
```
- **Clona y compila (mismos pasos que en red hat)**
```bash
git clone https://github.com/innotop/innotop.git
cd innotop
perl Makefile.PL
make
sudo make install
```
#### **3: Verificar la Instalación**

Una vez que la instalación esté completa, puedes verificar si innotop se ha instalado correctamente ejecutando:

`innotop --version`

#### **4: Usar Innotop**

Para comenzar a usar innotop, simplemente ejecuta el comando:

`innotop`

Esto te llevará a la interfaz de innotop, donde puedes conectarte a tu servidor MySQL o MariaDB y comenzar a monitorear el rendimiento.

