# Arquitectura de la Aplicación

## Visión General

La aplicación de Control de Citas y Asesorías utiliza una arquitectura de **3 capas**:

```
┌─────────────────────────────────────┐
│     Frontend (React/Next.js)        │
│  - UI Components                    │
│  - State Management (Redux/Zustand) │
│  - API Client (Axios/React Query)   │
└──────────────┬──────────────────────┘
               │ (HTTP/REST)
┌──────────────▼──────────────────────┐
│  Backend API (Node.js/Express)      │
│  - Routes & Controllers             │
│  - Business Logic                   │
│  - Middleware & Validación          │
│  - Authentication (JWT)             │
└──────────────┬──────────────────────┘
               │ (SQL)
┌──────────────▼──────────────────────┐
│  Database (PostgreSQL)              │
│  - Users, Appointments, Reviews    │
│  - Sessions, Advisors              │
└─────────────────────────────────────┘
```

## Componentes Principales

### 1. Frontend

#### Estructura de carpetas
```
frontend/
├── public/
├── src/
│   ├── components/       # Componentes reutilizables
│   │   ├── common/
│   │   ├── forms/
│   │   └── layout/
│   ├── pages/            # Páginas (Next.js)
│   ├── hooks/            # Custom hooks
│   ├── services/         # API calls
│   ├── store/            # Estado global
│   ├── types/            # TypeScript types
│   ├── utils/            # Funciones helper
│   ├── styles/           # Estilos globales
│   └── App.tsx
├── package.json
├── tsconfig.json
└── Dockerfile
```

#### Flujo de datos
1. Usuario interactúa con componente
2. Componente llama servicio API
3. Servicio hace request al backend
4. Respuesta se almacena en estado global
5. Componente se renderiza con nuevos datos

### 2. Backend

#### Estructura de carpetas
```
backend/
├── src/
│   ├── controllers/      # Lógica de requests
│   ├── services/         # Lógica de negocio
│   ├── models/           # Modelos Prisma
│   ├── routes/           # Definición de rutas
│   ├── middleware/       # Middleware (auth, validation)
│   ├── types/            # TypeScript interfaces
│   ├── utils/            # Funciones helper
│   ├── database/         # Configuración DB
│   ├── config/           # Configuración general
│   └── index.ts          # Entry point
├── prisma/
│   └── schema.prisma     # Esquema de BD
├── migrations/           # Migraciones SQL
├── package.json
├── tsconfig.json
└── Dockerfile
```

#### Flujo de request
1. Request llega a Express
2. Middleware de autenticación valida JWT
3. Middleware de validación comprueba datos
4. Controller procesa request
5. Service ejecuta lógica de negocio
6. Prisma interactúa con base de datos
7. Response se envía al cliente

### 3. Base de Datos

#### Tablas principales

**users**
- id (UUID)
- email
- password (hashed)
- firstName, lastName
- role (USER, ADVISOR)
- createdAt, updatedAt

**appointments**
- id (UUID)
- userId
- advisorId
- startTime
- endTime
- status (SCHEDULED, COMPLETED, CANCELLED)
- description
- createdAt, updatedAt

**advisors**
- id (UUID)
- userId
- specialization
- bio
- hourlyRate
- availabilitySlots (JSON)
- createdAt, updatedAt

**reviews**
- id (UUID)
- appointmentId
- rating
- comment
- createdAt

**sessions**
- id (UUID)
- appointmentId
- notes
- objectives
- nextSteps
- createdAt, updatedAt

## Flujo de Autenticación

```
1. Usuario hace login
   ↓
2. Backend valida credenciales
   ↓
3. Backend genera JWT token
   ↓
4. Frontend almacena token en localStorage
   ↓
5. Frontend incluye token en headers Authorization
   ↓
6. Backend valida token en cada request
   ↓
7. Si válido: continúa
   Si inválido: retorna 401 Unauthorized
```

## Seguridad

### Frontend
- Validación de formularios antes de enviar
- HTTPS only
- HttpOnly cookies para tokens (preferible)
- CSRF protection

### Backend
- Validación de input en todos los endpoints
- Rate limiting
- CORS configurado correctamente
- Passwords hashed con bcrypt
- Sanitización de datos
- SQL injection prevention (Prisma ORM)

### Base de datos
- Backups automáticos
- Encryption de datos sensibles
- Row-level security (RLS)

## Escalabilidad

### Estrategias

1. **Caching**
   - Redis para sesiones
   - CDN para assets estáticos

2. **Load Balancing**
   - Nginx/HAProxy
   - PM2 para procesos Node

3. **Database**
   - Connection pooling
   - Read replicas
   - Sharding si es necesario

4. **API**
   - GraphQL alternativo a REST
   - Pagination en listados
   - Lazy loading de datos

## Deployment

### Desarrollo
- Docker Compose local
- Hot reload de código

### Producción
- Docker en Kubernetes
- CI/CD con GitHub Actions
- Environment: AWS / Heroku / DigitalOcean
