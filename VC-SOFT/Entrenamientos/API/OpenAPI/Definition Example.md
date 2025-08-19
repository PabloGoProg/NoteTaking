## Secciones

1. **Metadatos del API**
	1. **`info`:** información (**metadatos**) general sobre la API.
	2. **`servers`:** URLs base desde donde se puede acceder a la API.
	3. **`tags`:** etiquetas para organizar y clasificar los endpoints por temas o funcionalidades.
	4. **`externalDocs`:** permite enlazar a documentación externa relacionada con el API.
2. **Elementos de Recursos** -> endpoint -> verbo
	1. **`parameters`:** valores, opcionales o requeridos que el cliente puede incluir en la URL o en los headers HTTP.
	2. **`requestBody`:** cuerpo del mensaje enviado en la solicitud, puede incluir el tipo de contenido (mime), esquema de validación para el contenido y ejemplos del mismo.
	3. **`responses`:** Define **las posibles respuestas** del servidor al llamar al endpoint, se diferencian según los códigos de respuesta posible e incluyen el tipo de contenido de la respuesta (mime), el esquema de validación de la salida y ejemplos del contenido.
3. **`components`:** hace referencia a los elementos reutilizables, los cuales pueden ser referenciados para evitar la duplicación de contenido en la definición.

```YAML
--> Posibles elementos de los components
components:
  schemas:           # ← Modelos de datos (objetos, arrays, strings, etc.)
  responses:         # ← Respuestas comunes predefinidas
  parameters:        # ← Parámetros reutilizables (query, header, path)
  examples:          # ← Ejemplos de objetos de entrada/salida
  requestBodies:     # ← Cuerpos de solicitud reutilizables
  headers:           # ← Headers HTTP comunes
  securitySchemes:   # ← Mecanismos de autenticación
```

```YAML
openapi: 3.0.0
info:
  title: simpleAPI
  description: >
    Esta es una API simple con un solo endpoint de login.
    Sirve como ejemplo para mostrar todos los elementos posibles en una definición de endpoint.
  version: 1.0.0
  termsOfService: https://simpleapi.example.com/terms
  contact:
    name: Soporte de simpleAPI
    email: soporte@simpleapi.example.com
    url: https://simpleapi.example.com/contacto
  license:
    name: MIT
    url: https://opensource.org/licenses/MIT

servers:
  - url: https://api.simpleapi.example.com/v1
    description: Servidor principal
  - url: http://localhost:3000
    description: Servidor local para testing

tags:
  - name: Auth
    description: Endpoints relacionados con autenticación

externalDocs:
  description: Documentación externa adicional
  url: https://simpleapi.example.com/docs

paths:
  /login:
    post:
      tags:
        - Auth
      summary: Iniciar sesión del usuario
      description: Este endpoint permite iniciar sesión mediante correo y contraseña.
      operationId: loginUser
      parameters:
        - in: query
          name: rememberMe
          schema:
            type: boolean
          description: Si se debe mantener la sesión iniciada
          required: false
          example: true
        - in: header
          name: X-Correlation-ID
          schema:
            type: string
          description: ID opcional para rastrear la solicitud
          required: false
          example: 123e4567-e89b-12d3-a456-426614174000
      requestBody:
        description: Credenciales de inicio de sesión
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/LoginRequest'
            examples:
              ejemploCorrecto:
                summary: Login exitoso
                value:
                  email: usuario@example.com
                  password: password123
      responses:
        '200':
          description: Login exitoso
          headers:
            Set-Cookie:
              description: Cookie de sesión
              schema:
                type: string
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/LoginResponse'
              examples:
                ejemplo200:
                  summary: Ejemplo de respuesta
                  value:
                    token: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
                    user:
                      id: 1
                      email: usuario@example.com
                      name: Juan Pérez
        '400':
          description: Error de validación
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ErrorResponse'
        '401':
          description: Credenciales inválidas
        '500':
          description: Error interno del servidor
      security: []

components:
  securitySchemes:
    basicAuth:
      type: http
      scheme: basic
    bearerAuth:
      type: http
      scheme: bearer
      bearerFormat: JWT

  schemas:
    LoginRequest:
      type: object
      required:
        - email
        - password
      properties:
        email:
          type: string
          format: email
          example: usuario@example.com
        password:
          type: string
          format: password
          example: password123
        callbackUrl:
          type: string
          format: uri
          example: https://cliente.example.com/callback

    LoginResponse:
      type: object
      properties:
        token:
          type: string
          description: Token JWT para autenticación futura
        user:
          $ref: '#/components/schemas/User'

    User:
      type: object
      properties:
        id:
          type: integer
          example: 1
        email:
          type: string
          format: email
        name:
          type: string

    ErrorResponse:
      type: object
      properties:
        error:
          type: string
        message:
          type: string
        code:
          type: integer
```