# LN-HostnameScreenPrint

Para las letras usaremos el programa figurine del repositorio: 
*https://github.com/arsham/figurine/releases*

**Descargar (linux en amd64):**
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

**Creamos el script en en update-motd.d**
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

**Permisos de ejecución**
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
