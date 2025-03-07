### **Reto 2: Flag Oculta en una Imagen con Mensaje Invisible**  
**Tema principal**: Esteganografía + Análisis Visual.

---

#### **Implementación Paso a Paso**

1. Crear una imagen básica (puedes usar cualquier editor gráfico):
   - Abrir GIMP o Photoshop.
   - Crear un archivo con fondo sólido (por ejemplo, blanco).
   - Escribir el texto: `Flag{Mensaje_Invisible}` en color blanco sobre el fondo blanco para hacerlo invisible.

2. Guardar la imagen como `reto.png`.

3. Verificar que el texto sea prácticamente imperceptible a simple vista.

4. Entregar el archivo `reto.png` al jugador como parte del desafío.

---

#### **Cómo lo resolverían los jugadores**

1. Abrir la imagen en un editor gráfico como GIMP o Photoshop.
2. Cambiar los niveles de contraste o brillo para hacer visible el texto oculto:
   - En GIMP: Ir a *Colores > Exposición* y ajustar los niveles.
   - En Photoshop: Usar *Ajustes > Brillo/Contraste*.

3. Alternativamente, usar herramientas de análisis como `strings` para inspeccionar el contenido binario:
   ```bash
   strings reto.png | grep "Flag"
   ```

4. Extraer la flag: `Flag{Mensaje_Invisible}`.

---

#### **Variantes para aumentar la dificultad**

- Utilizar esteganografía avanzada para ocultar el mensaje en los bits menos significativos (LSB) de la imagen:
  ```bash
  stegolsb encode -i reto.png -o reto_estego.png -s "Flag{Mensaje_Invisible}"
  ```
- Incluir múltiples capas de texto oculto con pistas adicionales que guíen al jugador hacia la flag final.
- Proteger el archivo con una contraseña y proporcionar pistas sobre cómo descifrarla.
