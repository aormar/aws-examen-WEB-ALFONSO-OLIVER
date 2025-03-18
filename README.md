# aws-examen-WEB-ALFONSO-OLIVER


## CREAR VPC EN AWS

### Paso 1: Crear VPC llamada: mi-vpc-TuNombre-Apellidos.

```bash

    Debemos iniciar sesión en nuestro laboratorio AWS
    Damos en START LAB y esperamos a que se ponga en verde
```
![alt text](/img/cap1.png)

```bash

    Dentro, buscamos el servicio VPC y entramos
    Vamos a crear una VPC, le damos para ello a CREAR VPC
```
![alt text](/img/cap2.png)

```bash

    Llamaremos a la VPC como mi-VPC-ALFONSO-OLIVERLIRIA
    El CIDR BLOCK sera la 10.0.0.0/16
    Una vez lo tengamos, la creamos.
```

![alt text](/img/cap3.png)

```bash

    A continuación, vamos a crear 2 subredes, una para Windows y otra para Linux
    Para ello, nos iremos al apartado de SUBREDES y daremos en CREAR SUBRED
    Empezaremos con la de Linux
```

![alt text](/img/cap4.png)

```bash

    Elegiremos la VPC creada anteriormente
    En el nombre de la Subred 1 pondremos subnet-linux con CIDR 10.0.1.0/24
    
```
![alt text](/img/cap5.png)

```bash

    En la Subred 2 pondremos subnet-windows con CIDR 10.0.2.0/24
    Al tenerlas configuradas, las crearemos
```

![alt text](/img/cap6.png)

```bash

    A continuación, vamos a crear una gateway asociada a nuestra VPC
    Nos vamos al apartado de Puerta de enlace de Internet
    Crear gateway de Internet
```

![alt text](/img/cap7.png)

```bash

    Le pondremos un nombre a la gateway y la creamos
```

![alt text](/img/cap8.png)

```bash

    Al crearla, nos saldrá un mensaje emergente en verde con un botón que dice
    "Asociar a VPC"
    Le damos y la asociaremos a nuestra VPC creada
```
![alt text](/img/cap9.png)
![alt text](/img/cap10.png)

```bash

    Comprobamos que se ha asociado correctamente
```

![alt text](/img/cap11.png)

```bash

    A continuación nos vamos a la tabla de enrutamiento y crearemos una
    Pondremos un nombre que la identifica y la asignamos a la VPC
```

![alt text](/img/cap12.png)
![alt text](/img/cap13.png)

```bash
    Una vez creada, daremos en EDITAR RUTAS
    Asignaremos la 0.0.0.0/0 a la Puerta de enlace de Internet anteriormente creada
    Comprobamos que se ha asignado correctamente
```

![alt text](/img/cap14.png)
![alt text](/img/cap15.png)

```bash
    Ahora vamos a asociar las dos subredes a la gateway
    Para ello nos vamos a Subredes, elegimos la primera y damos en Tabla de enrutamiento
    Editar la asociacion de la tabla de enrutamiento
    Asignamos la gateway y guardamos
    
```

![alt text](/img/cap16.png)
![alt text](/img/cap17.png)


```bash
    Haremos lo mismo con la segunda subred
```

![alt text](/img/cap18.png)


## CREACIÓN DE INSTANCIAS EN EC2

### INSTANCIA EC2 WINDOWS

```bash
    Ahora vamos a crear la instancia Windows
    Nos iremos al servicio EC2
    Daremos en Lanzar Instancia
```

![alt text](/img/cap19inswindows.png)

```bash
    Asignamos un nombre a la instancia
    Elegimos el sistema operativo "Windows"
    El tipo de Windows será "Windows-Server-2022 Base"
```

![alt text](/img/cap20inswindows.png)

```bash
    Tipo de instancia "t3.medium"
```
![alt text](/img/cap21inswindows.png)

```bash
    Creamos un par de claves RDA
```

![alt text](/img/cap22inswindows.png)

```bash
    Ahora vamos a editar la configuración de red
    Vamos a poner nuestra VPC, eligiendo la subred de windows
    Habilitamos la IP pública
    Asignamos un nombre al grupo de seguridad
```
![alt text](/img/cap23inswindows.png)

```bash
    Asignamos a continuación las reglas del grupo de seguridad
    HTTP puerto 80
    RDP puerto 3389
    VITE puerto 5173
```

![alt text](/img/cap24inswindows.png)

```bash
    Lanzamos la instancia
```

```bash
    Ahora crearemos la instancia de Linux siguiendo los mismos pasos
```

![alt text](/img/cap25inslinux.png)


```bash
    Tipo de instancia "t2.medium"
```
![alt text](/img/cap26inslinux.png)

```bash
    Generamos un par de claves para esta instancia
```

![alt text](/img/cap27inslinux.png)

```bash
    Ahora vamos a editar la configuración de red
    Vamos a poner nuestra VPC, eligiendo la subred de linux
    Habilitamos la IP pública
    Asignamos un nombre al grupo de seguridad
```

![alt text](/img/cap28inslinux.png)

```bash
    Asignamos a continuación las reglas del grupo de seguridad
    HTTP puerto 80
    SSH puerto 22
    VITE puerto 5173
```

![alt text](/img/cap29inslinux.png)

```bash
    Lanzamos la instancia
    Comprobamos que están las 2 instancias correctamente creadas y comprobadas
```
![alt text](/img/cap30.png)

## INSTALACIÓN Y DESPLIEGUE WEB

### UBUNTU SERVER

```bash
    Nos conectamos a la instancia de Linux
    Elegimos conectarnos con la clave SSH
    Tendremos que colocar estos comandos y se nos conectará:
    chmod 400 "claveLinux-Alfonso.pem
    ssh -i "claveLinux-Alfonso.pem" ubuntu@3.82.12.146
```

![alt text](/img/cap31inslinux.png)

```bash
    A continuación vamos a actualizar paquetes e instalar Node.js y npm
    Colocaremos los siguientes comandos:
    sudo apt update
    sudo apt install nodejs npm -y
```

![alt text](/img/cap32inslinux.png)
![alt text](/img/cap33inslinux.png)

```bash
    Una vez se instalen colocaremos el siguiente para instalar Vite y Serve:
    sudo npm install -g vite serve
```

![alt text](/img/cap34inslinux.png)

```bash
    Cuando se instale vamos a crear un proyecto con Vite
    mkdir web-tunombre-apellidos && cd web-tunombre-apellidos
    npm init vite@latest .
    npm install

```

![alt text](/img/cap35inslinux.png)

```bash
    Vamos a generar una build optimizada:
    npm run build
```

![alt text](/img/cap36inslinux.png)

```bash
    Por último servimos los archivos generados:
    serve -s dist -l 5173
```
![alt text](/img/cap43inslinux.png)

### WINDOWS SERVER

```bash
    Ahora lo haremos con la de Windows
    Conectamos nuestra instancia con el cliente RDP, descargando el archivo de escritorio remoto
```

![alt text](/img/cap40inswindows.png)

```bash
    Nos pedirá la contraseña, debemos descifrarla mediante nuestra clave anteriormente creada para Windows
    Comprobamos que se nos conecta
```

![alt text](/img/cap41inswindows.png)
![alt text](/img/cap42inswindows.png)



```bash
    Entramos en Powershell y anotaremos los siguientes comandos para instalar Node.js:
    Set-ExecutionPolicy Bypass -Scope Process -Force
    [System.Net.ServicePointManager]::SecurityProtocol = 'Tls12'
    Invoke-WebRequest -Uri https://nodejs.org/dist/v20.11.0/nodev20.11.0-x64.msi -OutFile node-installer.msi
    Se empezará a descargar

```

![alt text](/img/cap44inswindows.png)

```bash
    Pondremos el siguiente comando:
    Start-Process msiexec.exe -Wait -ArgumentList '/I nodeinstaller.msi /quiet'
    Si no hace nada ni nada error es que estamos haciendolo correctamente
```

![alt text](/img/cap45inswindows.png)

```bash
    Ahora instalaremos Vite y Serve con este comando:
    npm install -g vite serve
    "NO PUEDO INSTALAR PORQUE ME DA ESTE ERROR"
```
![alt text](/img/errorwindows.png)



## REGLAS ENTRANTES

```bash
    Vamos a editar las reglas de entrada creadas anteriormente en base a esto:
    HTTP (80) desde 0.0.0.0/0.
    Vite (5173) desde 0.0.0.0/0.
    SSH (22) desde tu IP pública (solo Linux).
    RDP (3389) desde tu IP pública (solo Windows).
```

![alt text](/img/cap37.png)
![alt text](/img/cap38.png)

## REGLAS SALIENTES

```bash
    Ahora las reglas salientes:
    Todo el tráfico permitido (0.0.0.0/0)
```

![alt text](/img/cap39.png)

