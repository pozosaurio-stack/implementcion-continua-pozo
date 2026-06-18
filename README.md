# Prisma Multiple Schemas - NestJS API

API moderna construida con **NestJS** y **Prisma ORM** que gestiona múltiples bases de datos independientes usando esquemas separados.

## 🏗️ Arquitectura

```
src/
├── modules/              # Módulos de dominio
│   ├── auth/            # Autenticación
│   ├── users/           # Gestión de usuarios
│   ├── subscriptions/   # Planes de suscripción
│   ├── music/           # Servicio de música
│   ├── likes/           # Sistema de likes
│   ├── matches/         # Matching de usuarios
│   └── chat/            # Mensajería
├── config/              # Configuración
│   └── prisma/          # Clientes Prisma (6 bases de datos)
└── common/              # Utilities compartidas
    └── utils/           # JWT, Password, Auth
```

## 🚀 Características

- ✅ **NestJS Framework** - Arquitectura moderna y escalable
- ✅ **Prisma ORM** - 6 bases de datos independientes
- ✅ **Validación** - DTOs con class-validator
- ✅ **Autenticación** - JWT integrado
- ✅ **Hashing** - Bcrypt para contraseñas
- ✅ **TypeScript** - Type-safe

## 📋 Requisitos

- Node.js >= 18
- npm o yarn
- PostgreSQL (u otra BD soportada)

## 🔧 Instalación

```bash
# Instalar dependencias
npm install

# Configurar variables de entorno
cp .env.example .env
# Editar .env con tus URLs de base de datos

# Generar clientes Prisma
npm run prisma:generate

# Crear migraciones
npm run prisma:migrate:create
```

## 🎯 Scripts Disponibles

```bash
# Desarrollo
npm run dev

# Build
npm run build

# Producción
npm start

# Prisma
npm run prisma:generate          # Generar clientes
npm run prisma:migrate:create    # Crear migraciones
npm run prisma:migrate:deploy    # Aplicar migraciones
npm run prisma:reset             # Resetear bases de datos
```

## 📡 Endpoints Principales

```
POST   /api/auth/register              # Registrarse
POST   /api/auth/login                 # Iniciar sesión
GET    /api/users                      # Listar usuarios
POST   /api/users                      # Crear usuario
GET    /api/users/:id                  # Obtener usuario
PUT    /api/users/:id                  # Actualizar usuario
DELETE /api/users/:id                  # Eliminar usuario

POST   /api/subscriptions/plans        # Crear plan
GET    /api/subscriptions/plans        # Listar planes

POST   /api/music/tracks               # Crear track
GET    /api/music/tracks               # Listar tracks

POST   /api/likes                       # Crear like
GET    /api/likes/sent/:userId         # Like enviados

POST   /api/matches                     # Crear match
GET    /api/matches/user/:userId       # Matches del usuario

POST   /api/chat                        # Crear chat
POST   /api/chat/messages              # Enviar mensaje
GET    /api/chat/user/:userId          # Chats del usuario
```

## 🗄️ Bases de Datos

El proyecto gestiona 6 bases de datos independientes:

1. **Users** - Usuarios y fotos
2. **Subscriptions** - Planes y suscripciones
3. **Music** - Tracks y preferencias
4. **Likes** - Sistema de likes
5. **Matches** - Matching entre usuarios
6. **Chat** - Mensajes y chats

Cada una con su propio esquema Prisma en `prisma/{module}/schema.prisma`

## 📦 Dependencias Principales

- `@nestjs/common` - Core NestJS
- `@nestjs/jwt` - JWT authentication
- `@prisma/client` - ORM
- `class-validator` - Validación de DTOs
- `bcryptjs` - Hashing de contraseñas
- `uuid` - Generación de IDs

## 🔐 Variables de Entorno

```env
PORT=3000
NODE_ENV=development

JWT_SECRET=your-secret-key
JWT_EXPIRES_IN=24h

DATABASE_URL_USERS=postgresql://...
DATABASE_URL_SUBSCRIPTIONS=postgresql://...
DATABASE_URL_MUSIC=postgresql://...
DATABASE_URL_LIKES=postgresql://...
DATABASE_URL_MATCHES=postgresql://...
DATABASE_URL_CHAT=postgresql://...
```

## 📝 Estructura de Módulos

Cada módulo sigue este patrón:

```
módulo/
├── dto/
│   └── index.ts           # Data Transfer Objects
├── módulo.controller.ts   # Controladores HTTP
├── módulo.service.ts      # Lógica de negocio
└── módulo.module.ts       # Configuración del módulo
```

## 🧪 Testing

Los módulos están preparados para testing con NestJS:

```bash
npm run test
npm run test:e2e
npm run test:cov
```

## 🤝 Contributing

Para contribuir:

1. Fork el repositorio
2. Crea una rama (`git checkout -b feature/AmazingFeature`)
3. Commit cambios (`git commit -m 'Add AmazingFeature'`)
4. Push a la rama (`git push origin feature/AmazingFeature`)
5. Abre un Pull Request

## 📄 Licencia

Este proyecto está bajo la licencia MIT.

## 👨‍💻 Autor

Desarrollado con NestJS y Prisma ORM.
