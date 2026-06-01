# Control de Citas y Asesorías

## Descripción
Aplicación para gestionar citas y asesorías a nivel profesional y personal. Sistema completo que permite organizar, programar y hacer seguimiento de sesiones de consultoría.

## Características

### Para Citas
- 📅 Calendario interactivo
- ⏰ Sistema de disponibilidad horaria
- ✅ Confirmación/cancelación automática
- 🔔 Recordatorios por email/SMS
- 📊 Estadísticas de ocupación

### Para Asesorías
- 👤 Perfiles de asesores
- 📝 Historial de sesiones
- 📋 Notas y seguimiento
- ⭐ Sistema de evaluación/feedback
- 🎯 Objetivos y metas de progreso

### General
- 🔐 Autenticación segura (JWT/OAuth)
- 📱 Interfaz responsiva
- 🌙 Modo oscuro
- 🔔 Sistema de notificaciones
- 📊 Dashboard con métricas
- 📤 Exportación de reportes

## Estructura del Proyecto

```
Control-de-Citas-y-Asesorias/
├── frontend/               # Aplicación React/Next.js
├── backend/                # API Node.js/Express
├── database/               # Scripts y migraciones SQL
├── docs/                   # Documentación
├── docker-compose.yml      # Configuración Docker
├── .gitignore
├── .env.example
└── README.md
```

## Stack Tecnológico

### Frontend
- React 18+ / Next.js 13+
- TypeScript
- Tailwind CSS
- React Query
- Zod (validación)

### Backend
- Node.js + Express
- TypeScript
- PostgreSQL
- Prisma ORM
- JWT Authentication
- Socket.io (notificaciones en tiempo real)

### Herramientas
- Docker & Docker Compose
- Git & GitHub
- GitHub Actions (CI/CD)

## Instalación

### Requisitos
- Node.js 18+
- PostgreSQL 14+
- Docker (opcional)

### Pasos

1. **Clonar repositorio**
```bash
git clone https://github.com/turhanfitzroy-debug/Control-de-Citas-y-Asesorias.git
cd Control-de-Citas-y-Asesorias
```

2. **Instalar dependencias**
```bash
# Frontend
cd frontend && npm install

# Backend
cd ../backend && npm install
```

3. **Configurar variables de entorno**
```bash
cp .env.example .env.local
# Editar .env.local con tus configuraciones
```

4. **Iniciar con Docker Compose**
```bash
docker-compose up -d
```

5. **Ejecutar migraciones**
```bash
cd backend
npm run migrate
```

## Desarrollo

### Ejecutar localmente

```bash
# Terminal 1: Backend
cd backend
npm run dev

# Terminal 2: Frontend
cd frontend
npm run dev
```

### API Documentation
La documentación de la API está disponible en `http://localhost:3001/api-docs`

## Fases de Desarrollo

### Fase 1: MVP (8 semanas)
- [ ] Autenticación de usuarios
- [ ] Dashboard básico
- [ ] CRUD de citas
- [ ] Calendario simple

### Fase 2: Core Features (8 semanas)
- [ ] Perfiles de asesores
- [ ] Sistema de disponibilidad
- [ ] Notificaciones email
- [ ] Historial de sesiones

### Fase 3: Advanced Features (8 semanas)
- [ ] Notificaciones en tiempo real
- [ ] Sistema de evaluación
- [ ] Reportes y estadísticas
- [ ] Integraciones (Zoom, Google Calendar)

## Contribuir

1. Crear una rama desde `develop`: `git checkout -b feature/nombre-feature`
2. Hacer commits descriptivos
3. Abrir un Pull Request hacia `develop`
4. Esperar revisión del código

## Licencia

MIT License - Ver [LICENSE](LICENSE) para más detalles

## Contacto

📧 Email: [tu-email@ejemplo.com]
🔗 LinkedIn: [tu-perfil]

---
**Última actualización**: Junio 2026
