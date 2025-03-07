### **Reto 1: Flag Oculta en un Archivo PDF**  
**Tema principal**: Análisis Forense + Manipulación de Archivos.

---

#### **Implementación Paso a Paso**

1. Crear un archivo PDF con texto genérico:
   ```bash
   echo "Este es un documento genérico para el reto CTF." > documento.txt
   pandoc documento.txt -o reto.pdf
   ```

2. Insertar la flag en los metadatos del archivo:
   ```bash
   exiftool -Author="Flag{PDF_Metadatos}" reto.pdf
   ```

3. Verificar que la flag esté correctamente oculta:
   ```bash
   exiftool reto.pdf
   ```

4. Entregar el archivo `reto.pdf` al jugador como parte del desafío.

---

#### **Cómo lo resolverían los jugadores**

1. Analizar los metadatos del archivo utilizando `exiftool`:
   ```bash
   exiftool reto.pdf
   ```

2. Buscar entre los campos de metadatos hasta encontrar el campo `Author` con la flag:  
   ```
   Author: Flag{PDF_Metadatos}
   ```

3. Extraer la flag y enviarla como solución.

---

#### **Variantes para aumentar la dificultad**

- Encriptar el archivo PDF con una contraseña y proporcionar pistas sobre cómo descifrarlo:
  ```bash
  qpdf --encrypt contraseña123 contraseña123 40 -- reto.pdf reto_encriptado.pdf
  ```
- Incrustar la flag dentro de un objeto oculto en el PDF, como una imagen invisible o un enlace.
