### **Reto 1: Flag Oculta en el Contenido de un PDF**  
**Tema principal**: Criptografía + Manipulación de Archivos.

---

#### **Implementación Paso a Paso**

1. Crear un archivo PDF con un párrafo donde la primera letra de cada línea forme la flag `MENSAJEOCULTO`:  
   Por ejemplo, el contenido del texto podría ser:  
   ```
   Mueve las piezas del desafío.  
   Encuentra la clave oculta.  
   Nunca subestimes los detalles.  
   Sigue las pistas cuidadosamente.  
   Analiza cada línea con atención.  
   Juega con lógica y precisión.  
   Explora todas las posibilidades.  
   Observa los patrones escondidos.  
   Comprende el mensaje cifrado.  
   Utiliza las herramientas adecuadas.  
   Lee entre líneas para resolverlo.  
   Toma tu tiempo para descifrarlo.  
   Observa el resultado final.  
   ```

2. Verificar que las primeras letras de cada línea formen correctamente la flag deseada (`MENSAJEOCULTO`) al abrir el archivo PDF.

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
3. Extraer la flag (en este caso, `MENSAJEOCULTO`) y enviarla como solución.

---

#### **Variantes para aumentar la dificultad**

- **Formato engañoso**: Cambiar el estilo del texto (por ejemplo, justificarlo o usar saltos de línea invisibles) para dificultar identificar las primeras letras.  
- **Encriptar el PDF con una contraseña** y proporcionar pistas para descifrarlo:
  ```bash
  qpdf --encrypt clave123 clave123 40 -- reto.pdf reto_encriptado.pdf
  ```
- **Ocultar pistas adicionales**: Incluir imágenes o enlaces invisibles en el PDF que distraigan al jugador.
