### **Reto 1: Flag Oculta en el Contenido de un PDF**  
**Tema principal**: Criptografía + Manipulación de Archivos.

---

#### **Implementación Paso a Paso**

1. Crear un archivo PDF con un párrafo donde la primera letra de cada línea forme la flag:  
   Por ejemplo, si la flag es `Flag{Texto_Oculto}`, el contenido del texto podría ser:  
   ```
   Frente a ti está el desafío.
   Lee con atención cada línea.
   Aquí está todo lo que necesitas.
   Gana descifrando el mensaje oculto.
   ```

   Generar el archivo `.txt` y convertirlo a PDF:
   ```bash
   echo -e "Frente a ti está el desafío.\nLee con atención cada línea.\nAquí está todo lo que necesitas.\nGana descifrando el mensaje oculto." > texto.txt
   pandoc texto.txt -o reto.pdf
   ```

2. Verificar que las primeras letras de cada línea formen correctamente la flag deseada (`Flag{Texto_Oculto}`) al abrir el archivo PDF.

3. Opcionalmente, añadir distracciones o pistas falsas:  
   - Agregar texto adicional irrelevante al documento.  
   - Incluir metadatos falsos para despistar:
     ```bash
     exiftool -Author="No hay nada aquí" reto.pdf
     ```

4. Entregar el archivo `reto.pdf` al jugador como parte del desafío.

---

#### **Cómo lo resolverían los jugadores**

1. Abrir y leer cuidadosamente el contenido del archivo PDF.  
2. Identificar que las primeras letras de cada línea forman un mensaje coherente (la flag).  
3. Extraer la flag (en este caso, `Flag{Texto_Oculto}`) y enviarla como solución.

---

#### **Variantes para aumentar la dificultad**

- **Formato engañoso**: Cambiar el estilo del texto (por ejemplo, justificarlo o usar saltos de línea invisibles) para dificultar identificar las primeras letras.  
- **Encriptar el PDF con una contraseña** y proporcionar pistas para descifrarlo:
  ```bash
  qpdf --encrypt clave123 clave123 40 -- reto.pdf reto_encriptado.pdf
  ```
- **Ocultar pistas adicionales**: Incluir imágenes o enlaces invisibles en el PDF que distraigan al jugador.  
