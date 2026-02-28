1. Proyecto - Sistema de Gestión de Estudiantes
Actividad 2
Estudiantes:
Paola Arismendy Johana Peña

1. Fork del repositorio
2. Configuración de la base de datos en la nube (Prisma.io)
postgres://d8040766bc1d1ea1fba3b00dfe7b5afaf69827cf9082acdc71b29abca9b81b9e: sk_t9aWgE9RFYp8uYJmOz3-g@db.prisma.io :5432/postgres?sslmode=require

3. Configuración del proyecto Spring Boot
URL de base de datos=jdbc:postgresql://db.prisma.io:5432/postgres?sslmode=require NOMBRE DE USUARIO DE BASE DE DATOS=d8040766bc1d1ea1fba3b00dfe7b5afaf69827cf9082acdc71b29abca9b81b9e CONTRASEÑA DE BASE DE DATOS=sk_5ihMS7v1oEHGmkQwikN7i

🚀 Guía de Pruebas y Documentación
1. Crear un nuevo estudiante
Método: POST
URL: http://localhost:8080/api/students
Cuerpo de Petición (JSON):
{
  "firstName": "Ana",
  "lastName": "García",
  "email": "ana.garcia@estudiante.com",
  "birthDate": "2001-03-12",
  "phone": "3004445566"
}
Respuesta del Servidor (Completar):
{
    "firstName": "Ana",
    "lastName": "García",
    "email": "ana.garcia@estudiante.com",
    "birthDate": "2001-03-12",
    "id": 2,
    "phone": "3004445566"
}
Código de Estado: 201 Created
2. Obtener la lista completa
Método: GET
URL: http://localhost:8080/api/students
Respuesta del Servidor (Completar):
[
    {
        "firstName": "Juan",
        "lastName": "Perez",
        "email": "juan.perez+test@example.com",
        "birthDate": "1995-06-15",
        "id": 1,
        "phone": "3001234567"
    },
      {
        "firstName": "Ana",
        "lastName": "García",
        "email": "ana.garcia@estudiante.com",
        "birthDate": "2001-03-12",
        "id": 2,
        "phone": "3004445566"
    }
]
Código de Estado: 200 OK
3. Buscar estudiante por ID (Existente)
Método: GET
URL: http://localhost:8080/api/students/1
Respuesta del Servidor (Completar):
{
    "firstName": "Juan",
    "lastName": "Perez",
    "email": "juan.perez+test@example.com",
    "birthDate": "1995-06-15",
    "id": 1,
    "phone": "3001234567"
}

Código de Estado: 200 OK
4. Buscar estudiante por correo electrónico
Método: GET
URL: http://localhost:8080/api/students/email/ana.garcia@estudiante.com
Respuesta del Servidor (Completar):
{
    "firstName": "Ana",
    "lastName": "García",
    "email": "ana.garcia@estudiante.com",
    "birthDate": "2001-03-12",
    "id": 2,
    "phone": "3004445566"
}

Código de Estado: 200 OK
5. Actualizar datos del estudiante
Método: PUT
URL: http://localhost:8080/api/students/1
Cuerpo de Petición (JSON):
{
  "firstName": "Ana María",
  "lastName": "García",
  "email": "ana.garcia@estudiante.com",
  "birthDate": "2001-03-12",
  "phone": "3119998877"
}
Respuesta del Servidor (Completar):
{
    "firstName": "Ana María",
    "lastName": "García",
    "email": "ana.garcia@estudiante.com",
    "birthDate": "2001-03-12",
    "id": 1,
    "phone": "3119998877"
}
Código de Estado: 200 OK
6. Escenario de error: Buscar ID inexistente
Método: GET
URL: http://localhost:8080/api/students/999
Respuesta del Servidor (Completar):
{
    "status": 404,
    "error": "Not Found",
    "message": "Student not found with id 999"
}
Código de Estado: 404 Not Found
7. Eliminar el registro
Método: DELETE
URL: http://localhost:8080/api/students/1
Respuesta del Servidor (Completar):
{}

Código de Estado: 204 No Content
📝 Cuestionario de Análisis
Instrucciones: Responda las siguientes preguntas basadas en su experiencia durante el laboratorio y el código del proyecto.

¿Cuál es la diferencia entre los códigos de estado 200 y 201? ¿En qué endpoints se obtuvo cada uno?
Respuesta: El 200 OK indica que la solicitud se procesó correctamente y se obtuvo el resultado esperado. El 201 Creado, en cambio, confirma que se generó un nuevo recurso en la base de datos. En el laboratorio, el 200 se recibió en consultas exitosas (por ejemplo, al listar estudiantes), mientras que el 201 apareció en los puntos finales de creación de registros.
En el escenario de error (punto 6), ¿qué información devuelve la API y por qué es importante para que un desarrollador frontend reciba un código 404 en lugar de un código 500?
Respuesta: La API devuelve un 404 Not Found, señalando que el recurso solicitado no existe. Esto es crucial para el frontend porque refleja un error del lado del cliente (un ID inexistente), mientras que un 500 Internal Server Error implicaría un fallo en el servidor. Diferenciar ambos ayuda a manejar mejor la experiencia del usuario y depurar el sistema.
¿Qué sucede en la base de datos PostgreSQL cuando se ejecuta con éxito la petición DELETE? (Explica brevemente en términos de persistencia).
Respuesta: Cuando la petición DELETE se ejecuta con éxito, el registro correspondiente se elimina de manera permanente de la base de datos. En términos de persistencia, significa que al realizar una consulta posterior con GET, ese ID ya no aparecerá porque dejó de existir en la tabla.
Si intentara crear un estudiante con el mismo correo electrónico que ya existe en la base de datos, ¿qué cree que sucedería y qué código de error sería el más adecuado para devolver?
Respuesta: Si se intenta registrar un estudiante con un correo ya existente, la base de datos rechaza la operación por violar la restricción de unicidad. El código más apropiado para devolver sería 409 Conflict, ya que refleja un conflicto entre la nueva solicitud y los datos previamente almacenados.
¿Por qué utilizamos el método PUT para actualizar y no el método POST? ¿Cuál es la convención técnica detrás de esta decisión?
Respuesta: La convención técnica dicta que POST se emplea para crear nuevos recursos, mientras que PUT se utiliza para actualizar uno existente identificado por su ID. Por eso, al modificar datos ya registrados, se recurre a PUT: la intención no es generar un recurso nuevo, sino reemplazar o actualizar el que ya está en la base.
