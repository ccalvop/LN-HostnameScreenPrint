# LN-HostnameScreenPrint

![image](https://github.com/user-attachments/assets/318d424c-29c9-41aa-8d68-e4c4ef290666)

# Personalización del Banner de Bienvenida en Linux

Personalizar el banner de bienvenida utilizando Figurine, una herramienta que genera texto ASCII art con distintas tipografías y colores. En lugar de tener el típico mensaje de texto plano al conectarnos a nuestro servidor, crearemos un banner más visual y dinámico que mostrará el hostname del servidor con un estilo distintivo.

## ¿Qué haremos?
1. Instalar Figurine
2. Configurar script que se ejecutará automáticamente
3. Personalizar el mensaje de bienvenida

## ¿Dónde se ejecutará?
El script puede configurarse en dos ubicaciones diferentes:
- `/etc/update-motd.d/`: Se mostrará como parte del banner inicial, antes del mensaje de "Last login"
- `/etc/profile.d/`: Se mostrará después del mensaje de "Last login"

Programa figurine en el repositorio: 
*https://github.com/arsham/figurine/releases*

***

## Pasos

**Descargamos la versión correcta (en mi caso linux en amd64):**
```console
wget https://github.com/arsham/figurine/releases/download/v1.3.0/figurine_linux_amd64_v1.3.0.tar.gz
```

**Descomprimir**
```console
tar -xvf figurine_linux_amd64_v1.3.0.tar.gz
```

**Mover a /usr/local/bin**
**Siguientes comando siendo root o añadiendo "sudo":*
```console
mv figurine /usr/local/bin/
```

**Descargamos el script (10-figurine.sh) de este repositorio**
```console
wget https://github.com/ccalvop/LN-HostnameScreenPrint/blob/main/10-figurine.sh
```

**O lo creamos en update-motd.d**

*El número "10" en el nombre del script (10-figurine) determina el orden de ejecución - los números más bajos se ejecutan primero.*
```console
nano /etc/update-motd.d/10-figurine
```

**Contenido del script**
```ssh
#!/bin/bash
echo ""
/usr/local/bin/figurine -f "3d.flf" "$(hostname)"
echo ""
```

**Aplicamos permisos de ejecución**
```console
chmod +x /etc/update-motd.d/10-figurine
```

**Notas:**

/etc/update-motd.d/: Forma parte del banner de bienvenida inicial

/etc/profile.d/: Se ejecuta cuando ya estás en la sesión

Secuencia de conexión:
1. [update-motd.d] "Este mensaje viene de update-motd.d"
2. Banner de Linux
3. Mensaje de copyright
4. Mensaje de Last login
5. [profile.d] "Este mensaje viene de profile.d"
