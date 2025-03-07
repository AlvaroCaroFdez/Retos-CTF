### **Reto 3: Flag Oculta en un Script Bash**  
**Tema principal**: Análisis de scripts + Ingeniería inversa.

---

#### **Implementación Paso a Paso**

1. Crear un script Bash con lógica ofuscada:
   ```bash
   #!/bin/bash

   # Función que genera la flag
   generar_flag() {
       local parte1="Flag"
       local parte2="{Bash"
       local parte3="_Analisis_Medio}"
       echo "$parte1$parte2$parte3"
   }

   # Mensaje inicial
   echo "Bienvenido al reto CTF. Encuentra la flag oculta."

   # Lógica ofuscada
   if [ "$1" == "--flag" ]; then
       echo "Acceso denegado."
   else
       echo "Pista: Analiza este script para encontrar lo que buscas."
   fi
   ```

2. Guardar el archivo como `reto.sh` y hacerlo ejecutable:
   ```bash
   chmod +x reto.sh
   ```

3. Entregar el archivo `reto.sh` al jugador como parte del desafío.

---

#### **Cómo lo resolverían los jugadores**

1. Inspeccionar el contenido del script:
   ```bash
   cat reto.sh
   ```

2. Identificar la función `generar_flag` y entender que genera la flag concatenando tres partes.

3. Ejecutar manualmente la función para revelar la flag:
   ```bash
   bash -c 'source reto.sh; generar_flag'
   ```

4. Extraer la flag: `Flag{Bash_Analisis_Medio}`.

---

#### **Variantes para aumentar la dificultad**

- Ofuscar aún más el código utilizando variables dinámicas:
  ```bash
  generar_flag() {
      local a="F"; local b="l"; local c="a"; local d="g"
      local e="{Bash_Analisis_Medio}"
      echo "$a$b$c$d$e"
  }
  ```

- Requerir un argumento específico para activar la generación de la flag:
  ```bash
  if [ "$1" == "--descifra" ]; then
      generar_flag
  fi
  ```

- Incluir funciones falsas o mensajes engañosos en el script para confundir al jugador.