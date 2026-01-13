# Elite Gypsum - Professional Gypsum Contractor Website

## Overview

A full-stack bilingual (English/Arabic) website for a gypsum board and ceiling contractor business. The application features a public-facing marketing website with services, projects, and contact information, plus a comprehensive admin control panel for content management. Built with React frontend, Express backend, PostgreSQL database (via Drizzle ORM), and optional MongoDB integration for extended CMS features.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture
- **Framework**: React 18 with TypeScript
- **Routing**: Wouter (lightweight router)
- **State Management**: TanStack React Query for server state
- **UI Components**: shadcn/ui (Radix UI primitives + Tailwind CSS)
- **Styling**: Tailwind CSS v4 with CSS variables for theming
- **Animations**: Framer Motion
- **Bilingual Support**: Custom language context with EN/AR translations stored in JSON locale files

### Backend Architecture
- **Runtime**: Node.js with Express
- **Language**: TypeScript (ESM modules)
- **Authentication**: Passport.js with Local Strategy, bcrypt for password hashing
- **Session Management**: express-session with cookie-based sessions
- **File Uploads**: Multer for media asset handling
- **API Structure**: RESTful endpoints organized by domain:
  - `/api/auth/*` - Authentication (login, register, logout, session check)
  - `/api/public/*` - Public content endpoints (settings, navigation, pages)
  - `/api/control-panel/*` - Admin CRUD operations (requires authentication)

### Data Storage

**Primary Database**: PostgreSQL with Drizzle ORM
- Schema defined in `shared/schema.ts`
- Tables: users, siteSettings, navigation, pages, formSubmissions, homeSections, services, projects, testimonials, footerSettings, mediaAssets
- All tables support bilingual content (En/Ar field variants)
- Database migrations via `drizzle-kit push`

**Secondary Database (Optional)**: MongoDB
- Connection manager in `server/db/mongodb.ts`
- Schema interfaces in `shared/mongodb-schema.ts`
- Used for extended CMS features like audit logs, analytics, and API keys
- Collections: siteSettings, navigation, pages, users, media, emailTemplates, analytics, apiKeys, auditLogs

### Storage Pattern
- Abstracted storage interface in `server/storage.ts`
- Implements repository pattern for all data operations
- Allows switching between PostgreSQL and MongoDB backends

### Build System
- **Development**: Vite dev server with HMR
- **Production**: Custom build script (`script/build.ts`) using esbuild for server, Vite for client
- **Output**: Server bundle to `dist/index.cjs`, client assets to `dist/public`

## External Dependencies

### Database Services
- **PostgreSQL**: Primary relational database (requires `DATABASE_URL` environment variable)
- **MongoDB Atlas**: Optional document database for extended features (requires `MONGODB_URI`)

### Third-Party Libraries
- **Drizzle ORM**: Database toolkit for PostgreSQL
- **Passport.js**: Authentication middleware
- **bcrypt**: Password hashing
- **Multer**: File upload handling
- **TanStack Query**: Data fetching and caching

### Replit-Specific Integrations
- `@replit/vite-plugin-runtime-error-modal`: Error overlay in development
- `@replit/vite-plugin-cartographer`: Development tooling
- `@replit/vite-plugin-dev-banner`: Development environment indicator

### Font Services
- Google Fonts: Playfair Display (headings), Manrope (body), Noto Sans Arabic (RTL support)

### Environment Variables Required
- `DATABASE_URL`: PostgreSQL connection string
- `MONGODB_URI`: MongoDB connection string (optional)
- `MONGODB_DB_NAME`: MongoDB database name (optional)
- `SESSION_SECRET`: Express session secret
- `PORT`: Server port (defaults to 5000)