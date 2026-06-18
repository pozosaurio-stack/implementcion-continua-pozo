# 📮 GUÍA DE POSTMAN PARA TESTING

## Instalación y Configuración

### 1. Descargar Postman
- Descarga desde: https://www.postman.com/downloads/
- O usa Postman Web: https://web.postman.co/

### 2. Importar Colección
1. Abre Postman
2. Click en **Import** (arriba a la izquierda)
3. Selecciona **Upload Files**
4. Elige: `POSTMAN_COLLECTION_NESTJS.json`
5. Click en **Import**

## Variables de Entorno

La colección usa 3 variables automáticas:

```
base_url    = http://localhost:3000  (URL base)
token       = (se obtiene al login)
userId      = (se obtiene al registrarse)
```

### Configuración Manual (opcional):
1. Click en **Environments** (arriba a la derecha)
2. Create → New Environment
3. Add variables:
   - base_url: http://localhost:3000
   - token: (vacío inicialmente)
   - userId: (vacío inicialmente)

## Flujo de Testing Recomendado

### Paso 1: Autenticación
```
1. POST /api/auth/register
   └─ Crea un nuevo usuario
   └─ Guarda automáticamente userId y token

2. POST /api/auth/login
   └─ Inicia sesión
   └─ Guarda automáticamente el token
```

### Paso 2: Usuarios
```
3. GET /api/users
   └─ Ver todos los usuarios

4. GET /api/users/{{userId}}
   └─ Ver usuario actual

5. PUT /api/users/{{userId}}
   └─ Actualizar datos del usuario

6. POST /api/users/photos
   └─ Agregar foto
```

### Paso 3: Suscripciones
```
7. POST /api/subscriptions/plans
   └─ Crear plan de suscripción

8. GET /api/subscriptions/plans
   └─ Ver planes disponibles

9. POST /api/subscriptions/assign
   └─ Asignar suscripción al usuario
```

### Paso 4: Música
```
10. POST /api/music/tracks
    └─ Crear track de música

11. GET /api/music/tracks
    └─ Ver todos los tracks

12. POST /api/music/add
    └─ Agregar música a usuario
```

### Paso 5: Likes
```
13. POST /api/likes
    └─ Crear like

14. GET /api/likes/sent/{{userId}}
    └─ Ver likes enviados

15. GET /api/likes/received/{{userId}}
    └─ Ver likes recibidos
```

### Paso 6: Matches
```
16. POST /api/matches
    └─ Crear match

17. GET /api/matches/user/{{userId}}
    └─ Ver matches del usuario

18. GET /api/matches/user/{{userId}}/active
    └─ Ver matches activos
```

### Paso 7: Chat
```
19. POST /api/chat
    └─ Crear chat

20. GET /api/chat/user/{{userId}}
    └─ Ver chats del usuario

21. POST /api/chat/messages
    └─ Enviar mensaje

22. GET /api/chat/messages/match-id
    └─ Ver mensajes del chat
```

## Consejos para Testing

### Auto-save de Variables
Los scripts de test en Postman guardan automáticamente:
- Al registrarse: `userId`
- Al login: `token` y `userId`

Ver respuesta en **Tests** de cada request.

### Headers Automáticos
Authorization header se agrega automáticamente en requests que lo requieran.

### Verificar Respuestas
1. Click en la request
2. Ver **Response** (abajo)
3. Tabs disponibles: Body, Headers, Cookies, Tests

### Troubleshooting

**Error: base_url not defined**
- Actualiza la variable en Environment
- Recarga la página

**Error: 404 Not Found**
- Verifica que el servidor está corriendo: `npm run dev`
- Comprueba la URL en la variable base_url

**Error: ECONNREFUSED**
- Servidor no está corriendo
- Ejecuta: `npm run dev`

**Error: 400 Bad Request**
- Revisa el body del request
- Verifica tipos de datos
- Lee el mensaje de error en Response

## Comandos Útiles

```bash
# Terminal 1: Iniciar servidor
npm run dev

# Terminal 2: Ver logs en tiempo real
npm run dev

# Generar clientes Prisma
npm run prisma:generate

# Ver Prisma Studio (interfaz gráfica BD)
npm run prisma:studio

# Resetear base de datos
npm run prisma:reset
```

## Endpoints Principales

### Autenticación
```
POST   /api/auth/register
POST   /api/auth/login
```

### Usuarios
```
POST   /api/users
GET    /api/users
GET    /api/users/:id
PUT    /api/users/:id
DELETE /api/users/:id
POST   /api/users/photos
GET    /api/users/:userId/photos
DELETE /api/users/photos/:photoId
```

### Suscripciones
```
POST   /api/subscriptions/plans
GET    /api/subscriptions/plans
GET    /api/subscriptions/plans/:id
PUT    /api/subscriptions/plans/:id
DELETE /api/subscriptions/plans/:id
POST   /api/subscriptions/assign
GET    /api/subscriptions/users/:userId/subscriptions
GET    /api/subscriptions/users/:userId/active
```

### Música
```
POST   /api/music/tracks
GET    /api/music/tracks
GET    /api/music/tracks/:id
PUT    /api/music/tracks/:id
DELETE /api/music/tracks/:id
POST   /api/music/add
GET    /api/music/users/:userId/music
DELETE /api/music/music/:id
```

### Likes
```
POST   /api/likes
GET    /api/likes
GET    /api/likes/sent/:userId
GET    /api/likes/received/:userId
GET    /api/likes/check/:senderUserId/:receiverUserId
DELETE /api/likes/:id
```

### Matches
```
POST   /api/matches
GET    /api/matches
GET    /api/matches/:id
PUT    /api/matches/:id
GET    /api/matches/user/:userId
GET    /api/matches/user/:userId/active
DELETE /api/matches/:id
```

### Chat
```
POST   /api/chat
GET    /api/chat
GET    /api/chat/:id
GET    /api/chat/between?user1Id=x&user2Id=y
GET    /api/chat/user/:userId
PUT    /api/chat/:id
DELETE /api/chat/:id
POST   /api/chat/messages
GET    /api/chat/messages/:matchId
PUT    /api/chat/messages/:id/read
DELETE /api/chat/messages/:id
GET    /api/chat/messages/:matchId/unread-count
```

### Health
```
GET    /health
GET    /
```

## ¡Listo para Testing! 🚀

1. Asegúrate que el servidor esté corriendo: `npm run dev`
2. Importa la colección en Postman
3. Comienza con Autenticación → Registrarse
4. Sigue el flujo recomendado
5. ¡Disfruta testing! 😊
