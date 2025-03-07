### **Reto 4: Flag Oculta en una API Vulnerable**  
**Tema principal**: Explotación de APIs + Ingeniería inversa.

---

#### **Implementación Paso a Paso**

1. Crear una API simulada utilizando Flask:
   ```python
   from flask import Flask, jsonify, request

   app = Flask(__name__)

   # Datos simulados
   usuarios = [
       {"id": 1, "nombre": "admin", "email": "admin@example.com", "flag": "Flag{API_Vulnerable}"},
       {"id": 2, "nombre": "user", "email": "user@example.com"}
   ]

   @app.route("/api/usuarios", methods=["GET"])
   def obtener_usuarios():
       # Vulnerabilidad: Exposición excesiva de datos
       return jsonify(usuarios)

   @app.route("/api/usuario/", methods=["GET"])
   def obtener_usuario(id):
       usuario = next((u for u in usuarios if u["id"] == id), None)
       if usuario:
           return jsonify(usuario)
       return jsonify({"error": "Usuario no encontrado"}), 404

   if __name__ == "__main__":
       app.run(debug=True)
   ```

2. Guardar el archivo como `reto_api.py` y ejecutarlo:
   ```bash
   python3 reto_api.py
   ```

3. Entregar al jugador la URL base de la API (`http://localhost:5000/api`) y pedirle que explore los endpoints.

---

#### **Cómo lo resolverían los jugadores**

1. Explorar el endpoint `/api/usuarios` utilizando herramientas como `curl`:
   ```bash
   curl http://localhost:5000/api/usuarios
   ```
   Respuesta:
   ```json
   [
       {"id": 1, "nombre": "admin", "email": "admin@example.com", "flag": "Flag{API_Vulnerable}"},
       {"id": 2, "nombre": "user", "email": "user@example.com"}
   ]
   ```

2. Identificar que el campo `flag` está expuesto en el objeto del usuario `admin`.

3. Extraer la flag: `Flag{API_Vulnerable}`.

4. Alternativamente, explorar el endpoint `/api/usuario/1` para obtener los datos del usuario específico:
   ```bash
   curl http://localhost:5000/api/usuario/1
   ```
   Respuesta:
   ```json
   {
       "id": 1,
       "nombre": "admin",
       "email": "admin@example.com",
       "flag": "Flag{API_Vulnerable}"
   }
   ```

---

#### **Variantes para aumentar la dificultad**

- Requerir autenticación básica o tokens JWT para acceder a los endpoints:
  ```python
  from flask import Flask, jsonify, request

  # Añadir lógica de autenticación básica aquí...
  ```

- Incluir datos cifrados en las respuestas:
  - Cifrar el valor del campo `flag` utilizando Base64 o XOR.
  - Obligar al jugador a descifrarlo manualmente:
    ```python
    import base64

    usuarios = [
        {"id": 1, "nombre": "admin", "email": "admin@example.com", 
         "flag": base64.b64encode(b"Flag{API_Vulnerable}").decode()}
    ]
    ```

- Introducir múltiples endpoints con pistas falsas para confundir al jugador.