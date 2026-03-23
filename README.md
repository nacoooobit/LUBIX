# 🚀 Lubix - Plataforma de Gestión de Usuarios y Empresas

Lubix es una **plataforma completa** de e-commerce, con un backend robusto y un frontend moderno y responsivo.

## 📋 Descripción General

Lubix permite a los usuarios:
- 👤 Registrarse e iniciar sesión
- 🏢 Crear y gestionar empresas
- 👥 Gestionar usuarios de su empresa
- 📊 Ver dashboards con estadísticas
- 🔐 Autenticación segura con JWT

## 🏗️ Estructura del Proyecto

```
proyecto/
├── LUBIX-BACKEND/          # Backend con FastAPI + SQLAlchemy
│   ├── app/
│   │   ├── main.py         # Punto de entrada FastAPI
│   │   ├── config.py       # Configuración
│   │   ├── database/       # Conexión a BD
│   │   ├── models/         # Modelos SQLAlchemy (Users, Companies)
│   │   ├── routers/        # Endpoints (user_routers.py, health.py)
│   │   ├── schemas/        # Validación con Pydantic
│   │   └── utils/          # JWT, test database
│   ├── requirements.txt    # Dependencias Python
│   └── README.md           # Documentación backend
│
├── LUBIX-FRONTED/frontend/        # Frontend con React + Vite
│   ├── src/
│   │   ├── pages/          # Login, Register, Home
│   │   ├── components/     # Componentes reutilizables
│   │   ├── services/       # API calls, autenticación
│   │   ├── App.tsx         # Componente raíz
│   │   └── main.tsx        # Punto de entrada
│   ├── package.json        # Dependencias NPM
│   ├── tailwind.config.js  # Tailwind CSS config
│   └── README.md           # Documentación frontend
│
├── .git/                   # Repositorio Git
├── .gitignore              # Archivos ignorados
└── README.md               # Este archivo

```

## 🛠️ Stack Tecnológico

### Backend
- **FastAPI** — Framework web rápido y moderno
- **SQLAlchemy** — ORM para manejo de base de datos
- **Pydantic** — Validación de datos
- **JWT** — Autenticación segura
- **SQLite/PostgreSQL** — Base de datos

### Frontend
- **React 19.2.4** — Librería UI
- **TypeScript 5.9** — Type safety
- **Vite 8.0** — Build tool rápido
- **Tailwind CSS 3.4** — Estilos utilitarios
- **React Router 6.30** — Enrutamiento
- **Axios 1.7** — Cliente HTTP

## 🚀 Cómo Iniciar

### 1️⃣ Backend (FastAPI)

```bash
cd LUBIX-BACKEND

# Instalar dependencias
pip install -r requirements.txt

# O con pip de Windows
pip install fastapi uvicorn sqlalchemy pydantic python-dotenv

# Ejecutar servidor
python -m uvicorn app.main:app --reload

# El servidor estará en: http://localhost:8000
# Documentación: http://localhost:8000/docs
```

**Puerto:** `8000`  
**Documentación interactiva:** http://localhost:8000/docs

### 2️⃣ Frontend (React + Vite)

```bash
cd LUBIX-FRONTED/frontend

# Instalar dependencias
npm install

# Ejecutar en desarrollo
npm run dev

# El servidor estará en: http://localhost:5173
```

**Puerto:** `5173`

## 📡 Endpoints del Backend

### Autenticación
- `POST /auth/register` — Registrar usuario
- `POST /auth/login` — Iniciar sesión
- `POST /auth/logout` — Cerrar sesión

### Usuarios
- `GET /users` — Listar usuarios
- `GET /users/{id}` — Obtener usuario por ID
- `POST /users` — Crear usuario
- `PUT /users/{id}` — Actualizar usuario
- `DELETE /users/{id}` — Eliminar usuario

### Empresas
- `GET /companies` — Listar empresas
- `GET /companies/{id}` — Obtener empresa por ID
- `POST /companies` — Crear empresa
- `PUT /companies/{id}` — Actualizar empresa
- `DELETE /companies/{id}` — Eliminar empresa

### Health Check
- `GET /health` — Verificar estado del servidor

## 🌐 Rutas del Frontend

| Ruta | Página | Descripción |
|------|--------|-------------|
| `/` | Login | Iniciar sesión |
| `/register` | Register | Crear cuenta |
| `/home` | Home | Dashboard principal |
| `/users` | Users | Gestión de usuarios |
| `/companies` | Companies | Gestión de empresas |
| `/perfil` | Profile | Perfil del usuario |

## 🔄 Flujo de Autenticación

```
Usuario
  ↓
[Login Page] — sin cuenta → [Register Page]
  ↓                              ↓
  validar credenciales    crear cuenta
  ↓                              ↓
[GET /auth/login]          [POST /auth/register]
  ↓                              ↓
obtener JWT              ir a Login →
  ↓                        [GET /auth/login]
[Home Dashboard]               ↓
                           obtener JWT
                               ↓
                           [Home Dashboard]
```

## 📝 Modelos de Datos

### Usuario
```json
{
  "id": 1,
  "nombre": "Juan Pérez",
  "email": "juan@email.com",
  "password": "hashed_password",
  "empresa_id": 1,
  "creado_en": "2026-03-23T10:30:00",
  "activo": true
}
```

### Empresa
```json
{
  "id": 1,
  "nombre": "Acme Inc",
  "descripcion": "Empresa de tecnología",
  "email": "info@acme.com",
  "telefono": "+1234567890",
  "direccion": "Calle Principal 123",
  "creado_en": "2026-03-23T10:30:00",
  "activo": true
}
```

## 🔐 Seguridad

- 🔒 **JWT Tokens** — Autenticación sin sesiones
- 🔑 **Contraseñas hasheadas** — Usando bcrypt o similar
- 🛡️ **CORS habilitado** — Para comunicación frontend-backend
- ✅ **Validación de entrada** — Pydantic schemas
- 🚫 **SQL Injection prevention** — SQLAlchemy ORM

## 🛠️ Configuración

### Variables de Entorno

Crear archivo `.env` en **LUBIX-BACKEND/**:

```env
DATABASE_URL=sqlite:///./lubix.db
SECRET_KEY=your-secret-key-here-change-in-production
ALGORITHM=HS256
ACCESS_TOKEN_EXPIRE_MINUTES=30
```

### CORS

El backend permite requests desde `http://localhost:5173` (frontend).

**Para producción:** Cambiar la URL del frontend en `app/main.py`

## 📦 Dependencias

### Backend (`requirements.txt`)
```
fastapi==0.104.1
uvicorn==0.24.0
sqlalchemy==2.0.23
pydantic==2.5.0
python-jose==3.3.0
passlib==1.7.4
python-dotenv==1.0.0
```

### Frontend (`package.json`)
```json
{
  "dependencies": {
    "react": "^19.2.4",
    "react-dom": "^19.2.4",
    "react-router-dom": "^6.30.3",
    "axios": "^1.7.7"
  },
  "devDependencies": {
    "tailwindcss": "^3.4.19",
    "vite": "^8.0.1",
    "typescript": "~5.9.3"
  }
}
```

## 🧪 Testing

### Backend
```bash
cd LUBIX-BACKEND
python -m pytest tests/
```

### Frontend
```bash
cd LUBIX-FRONTED/frontend
npm run test
```

## 🚢 Despliegue

### Backend (Vercel, Render, Heroku)
```bash
# Build para producción
uvicorn app.main:app --host 0.0.0.0 --port 8000
```

### Frontend (Vercel, Netlify)
```bash
cd frontend
npm run build
# Carpeta 'dist/' lista para deploy
```

## 📚 Documentación Adicional

- [Backend README](./LUBIX-BACKEND/README.md)
- [Frontend README](./LUBIX-FRONTED/frontend/README.md)

## 🤝 Contribuir

1. Fork el repositorio
2. Crea una rama: `git checkout -b feature/mi-feature`
3. Cambios: `git commit -m 'Add: descripción'`
4. Push: `git push origin feature/mi-feature`
5. Pull Request

## 📞 Soporte

- ¿Preguntas? Abre un issue en el repositorio
- ¿Bugs? Reporta con detalles en GitHub Issues
- ¿Sugerencias? Usa Discussions

## 📄 Licencia

Este proyecto está bajo licencia MIT. Ver archivo `LICENSE`.

## 🎯 Roadmap

### v1.1 (Próximo)
- [ ] Dashboard con gráficos
- [ ] Exportar datos a Excel/PDF
- [ ] 2FA (Two-Factor Authentication)
- [ ] Notificaciones por email

### v1.2 (Futuro)
- [ ] API GraphQL
- [ ] Mobile app (React Native)
- [ ] Integración con terceros
- [ ] Sistema de permisos avanzado

## 👥 Equipo

- **Desarrollador Principal:** Johann
- **Última actualización:** Marzo 2026

---

**¡Gracias por usar Lubix!** 🎉

Para más información, visita la documentación de cada módulo.
