# Code Snippet Manager - MERN Stack

A secure, and scalable code snippet vault with multi-language support, syntax highlighting, tag-based organization, visibility controls, forking, and safe code execution preview.

## 🚀 Features

- **Snippet Management**: Full CRUD operations with rich metadata (title, description, tags, language)
- **Syntax Highlighting**: Monaco editor for editing, Prism for read views
- **Search & Discovery**: Tag-based search, language filters, full-text search
- **Fork System**: Clone public snippets with lineage tracking
- **Visibility Control**: Public, private, and unlisted snippets
- **Safe Execution**: Sandboxed code execution with resource limits
- **Authentication**: JWT-based auth with access and refresh tokens
- **Collections**: Organize snippets into folders
- **Social Features**: Stars, views, activity tracking

## 🏗️ Architecture

- **Frontend**: React 18 + TypeScript + Vite
- **Backend**: Node.js + Express + TypeScript
- **Database**: MongoDB with Mongoose ODM
- **Authentication**: JWT (access + refresh tokens)
- **Code Editor**: Monaco Editor
- **Syntax Highlighting**: Prism.js
- **Execution Sandbox**: Docker-based isolated runners
- **Testing**: Jest, React Testing Library, Supertest
- **CI/CD**: GitHub Actions
- **Monitoring**: Sentry, Prometheus

## 📋 Prerequisites

- Node.js >= 18.x
- MongoDB >= 6.x
- Docker (for execution sandbox)
- npm or yarn

## 🛠️ Installation

### 1. Clone and Install Dependencies

```bash
# Install backend dependencies
cd backend
npm install

# Install frontend dependencies
cd ../frontend
npm install
```

### 2. Environment Configuration

Create `.env` files in both backend and frontend directories:

**backend/.env**
```env
NODE_ENV=development
PORT=5000
MONGODB_URI=mongodb://localhost:27017/snippet-manager
JWT_ACCESS_SECRET=your-access-secret-key-change-in-production
JWT_REFRESH_SECRET=your-refresh-secret-key-change-in-production
JWT_ACCESS_EXPIRY=15m
JWT_REFRESH_EXPIRY=7d
CORS_ORIGIN=http://localhost:5173
RUNNER_API_URL=http://localhost:5001
SENTRY_DSN=
RATE_LIMIT_WINDOW_MS=900000
RATE_LIMIT_MAX_REQUESTS=100
```

**frontend/.env**
```env
VITE_API_URL=http://localhost:5000/api
VITE_SENTRY_DSN=
```

### 3. Start MongoDB

```bash
# Using Docker
docker run -d -p 27017:27017 --name mongodb mongo:latest

# Or use MongoDB Atlas (cloud)
```

### 4. Run the Application

```bash
# Terminal 1: Start backend
cd backend
npm run dev

# Terminal 2: Start frontend
cd frontend
npm run dev

# Terminal 3: Start execution runner (optional)
cd backend/runner
npm run dev
```

The application will be available at:
- Frontend: http://localhost:5173
- Backend API: http://localhost:5000
- API Docs: http://localhost:5000/api-docs

## 🧪 Testing

```bash
# Backend tests
cd backend
npm test
npm run test:coverage

# Frontend tests
cd frontend
npm test
npm run test:e2e

# Integration tests
npm run test:integration
```

## 🚢 Deployment

### Using Docker

```bash
# Build and run all services
docker-compose up -d

# Scale runner workers
docker-compose up -d --scale runner=3
```

### Manual Deployment

1. **Build frontend**:
   ```bash
   cd frontend
   npm run build
   ```

2. **Deploy backend**: Upload to your hosting provider (AWS, Heroku, etc.)

3. **Configure environment variables** in production

4. **Set up MongoDB Atlas** or managed MongoDB instance

5. **Configure CDN** for frontend static assets

## 📚 API Documentation

API documentation is available via Swagger UI at `/api-docs` when running the backend.

### Key Endpoints

- **Auth**: `/api/auth/register`, `/api/auth/login`, `/api/auth/refresh`
- **Snippets**: `/api/snippets` (CRUD operations)
- **Search**: `/api/search?q=term&language=javascript&tags=react`
- **Fork**: `POST /api/snippets/:id/fork`
- **Execute**: `POST /api/snippets/:id/execute`
- **Collections**: `/api/collections` (CRUD)

## 🔒 Security

- Passwords hashed with bcrypt (cost factor 12)
- JWT tokens with short expiry
- Rate limiting on all endpoints
- Input validation with Zod
- CORS protection
- XSS prevention
- SQL/NoSQL injection prevention
- Sandboxed code execution with resource limits
- Audit logging for sensitive operations

## 🎨 Tech Stack

### Backend
- Node.js + Express
- TypeScript
- MongoDB + Mongoose
- JWT authentication
- Joi/Zod validation
- bcrypt
- helmet (security headers)
- express-rate-limit
- morgan (logging)

### Frontend
- React 18
- TypeScript
- Vite
- React Router v6
- Zustand (state management)
- Monaco Editor
- Prism.js
- TailwindCSS
- shadcn/ui components
- Axios
- React Hook Form

### DevOps
- Docker + Docker Compose
- GitHub Actions
- ESLint + Prettier
- Jest + Supertest
- Cypress/Playwright

## 📖 Project Structure

```
MERN_Project/
├── backend/
│   ├── src/
│   │   ├── config/         # Configuration files
│   │   ├── models/         # Mongoose models
│   │   ├── controllers/    # Route controllers
│   │   ├── routes/         # Express routes
│   │   ├── middleware/     # Custom middleware
│   │   ├── services/       # Business logic
│   │   ├── utils/          # Utility functions
│   │   └── server.ts       # Entry point
│   ├── tests/              # Test files
│   ├── runner/             # Execution sandbox service
│   └── package.json
├── frontend/
│   ├── src/
│   │   ├── components/     # React components
│   │   ├── pages/          # Page components
│   │   ├── hooks/          # Custom hooks
│   │   ├── store/          # State management
│   │   ├── services/       # API services
│   │   ├── utils/          # Utilities
│   │   └── App.tsx         # Root component
│   ├── public/
│   └── package.json
├── docker-compose.yml
└── README.md
```

## 🐛 Troubleshooting

### MongoDB Connection Failed
- Ensure MongoDB is running: `mongosh` or check Docker container
- Verify MONGODB_URI in `.env`

### Port Already in Use
- Change PORT in backend `.env`
- Update VITE_API_URL in frontend `.env`

### Execution Sandbox Not Working
- Ensure Docker is running
- Check runner service logs: `docker logs snippet-runner`

