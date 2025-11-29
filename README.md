# 🎵 Music Platform

A modern, full-stack music streaming platform built with **Rust** (Axum) backend and **Next.js 14** frontend, featuring real-time WebSocket communication, secure authentication, and a beautiful user interface.

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![Rust](https://img.shields.io/badge/rust-%23000000.svg?style=flat&logo=rust&logoColor=white)
![Next.js](https://img.shields.io/badge/Next.js-000000?style=flat&logo=next.js&logoColor=white)
![TypeScript](https://img.shields.io/badge/typescript-%23007ACC.svg?style=flat&logo=typescript&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/postgresql-%23316192.svg?style=flat&logo=postgresql&logoColor=white)

## ✨ Features

- 🎧 **Real-time Audio Streaming** - High-quality audio playback with WebSocket support
- 🔐 **Secure Authentication** - JWT-based authentication with session management
- 🎨 **Modern UI** - Beautiful, responsive interface built with ShadCN and Tailwind CSS
- ⚡ **High Performance** - Rust-powered backend with HTTP/2 support
- 🌐 **WebSocket Support** - Real-time features for live streaming and chat
- 📱 **Responsive Design** - Optimized for desktop and mobile devices
- 🎵 **Multi-format Support** - AAC, FLAC, MP3, WAV, and OGG audio formats
- 🔒 **HTTPS Support** - Secure connections with TLS/SSL

## 🏗️ Architecture

This project follows a modern full-stack architecture:

```
music_platform/
├── backend/          # Rust (Axum) API server
│   ├── src/
│   │   ├── handler/  # Request handlers
│   │   ├── database/ # Database models and queries
│   │   ├── utils/    # Utility functions
│   │   └── main.rs   # Application entry point
│   ├── migrations/   # Database migrations
│   └── certs/        # SSL/TLS certificates
│
└── frontend/         # Next.js 14 application
    ├── app/          # Next.js app router
    ├── components/   # React components
    ├── action/       # Server actions
    └── lib/          # Utility libraries
```

## 🛠️ Tech Stack

### Backend
- **Framework:** [Axum](https://github.com/tokio-rs/axum) - High-performance web framework for Rust
- **Database:** PostgreSQL with [SQLx](https://github.com/launchbadge/sqlx) - Async, compile-time checked queries
- **Authentication:** JWT (jsonwebtoken) with Argon2 password hashing
- **Real-time:** WebSockets (tokio-tungstenite)
- **Audio Processing:** Symphonia - Pure Rust audio decoder
- **Async Runtime:** Tokio - Asynchronous runtime for Rust
- **HTTPS:** axum-server with TLS-rustls

### Frontend
- **Framework:** [Next.js 14](https://nextjs.org/) - React framework with App Router
- **Language:** TypeScript - Type-safe development
- **UI Components:** [ShadCN](https://ui.shadcn.com/) - Radix UI-based component library
- **Styling:** [Tailwind CSS](https://tailwindcss.com/) - Utility-first CSS framework
- **Form Handling:** React Hook Form with Zod validation
- **Audio Playback:** Howler.js - JavaScript audio library
- **Real-time:** Socket.IO Client - WebSocket communication
- **Theme:** next-themes - Dark/light mode support

## 📋 Prerequisites

Before you begin, ensure you have the following installed:

- **Rust** (latest stable) - [Install Rust](https://www.rust-lang.org/tools/install)
- **Node.js** (v18 or later) - [Install Node.js](https://nodejs.org/)
- **PostgreSQL** (v14 or later) - [Install PostgreSQL](https://www.postgresql.org/download/)
- **npm** or **yarn** - Package manager

## 🚀 Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/ssebide/music-platform.git
cd music_platform
```

### 2. Backend Setup

#### Install Dependencies

```bash
cd backend
cargo build
```

#### Configure Environment Variables

Create a `.env` file in the `backend` directory:

```env
# Database Configuration
DATABASE_URL=postgresql://username:password@localhost:5432/music

# JWT Configuration
JWT_SECRET_KEY=your_ultra_secure_jwt_secret_key_here
JWT_MAXAGE=60
```

#### Run Database Migrations

```bash
sqlx migrate run
```

#### Generate SSL Certificates (Optional)

For local HTTPS development, generate self-signed certificates:

```bash
# Linux/macOS
openssl req -x509 -newkey rsa:4096 -nodes -keyout certs/key.pem -out certs/cert.pem -days 365

# Windows (using Git Bash or WSL)
openssl req -x509 -newkey rsa:4096 -nodes -keyout certs/key.pem -out certs/cert.pem -days 365
```

#### Start the Backend Server

```bash
cargo run
```

The backend server will start on `https://localhost:8000` (or your configured port).

### 3. Frontend Setup

#### Install Dependencies

```bash
cd ../frontend
npm install
# or
yarn install
```

#### Configure Environment Variables

Create a `.env` file in the `frontend` directory:

```env
API_BASE_URL=https://localhost:8000/api
```

#### Start the Development Server

```bash
npm run dev
# or
yarn dev
```

The frontend will start on `https://localhost:3000`.

## 📁 Project Structure

### Backend Structure

```
backend/
├── src/
│   ├── handler/      # API endpoint handlers
│   ├── database/     # Database models and operations
│   ├── utils/        # Helper utilities
│   ├── auth.rs       # Authentication logic
│   ├── config.rs     # Configuration management
│   ├── dtos.rs       # Data Transfer Objects
│   ├── error.rs      # Error handling
│   ├── models.rs     # Domain models
│   ├── routes.rs     # Route definitions
│   └── main.rs       # Application entry point
├── migrations/       # Database migration files
├── certs/           # SSL/TLS certificates
└── Cargo.toml       # Rust dependencies
```

### Frontend Structure

```
frontend/
├── app/             # Next.js app router pages
├── components/      # React components
│   ├── ui/         # ShadCN UI components
│   └── ...         # Custom components
├── action/          # Server actions
├── lib/            # Utility libraries
├── certificates/   # SSL certificates for development
└── package.json    # Node.js dependencies
```

## 🔌 API Endpoints

### Authentication

- `POST /api/auth/register` - Register a new user
- `POST /api/auth/login` - Login user
- `POST /api/auth/logout` - Logout user
- `GET /api/auth/me` - Get current user

### Music

- `GET /api/songs` - Get all songs
- `GET /api/songs/:id` - Get song by ID
- `POST /api/songs` - Upload new song (requires authentication)
- `DELETE /api/songs/:id` - Delete song (requires authentication)
- `GET /api/stream/:id` - Stream audio file

### WebSocket

- `WS /ws` - WebSocket connection for real-time features

## 🎨 UI Components

The frontend utilizes ShadCN components for a consistent, accessible UI:

- **Audio Player** - Custom-built music player with playlist support
- **Navigation** - Responsive navigation with dark mode toggle
- **Forms** - Validated forms for authentication and uploads
- **Dialogs** - Modal dialogs for actions and confirmations
- **Progress Bars** - Visual feedback for audio playback
- **Sliders** - Volume and seek controls

## 🧪 Testing

### Backend Tests

```bash
cd backend
cargo test
```

### Frontend Tests

```bash
cd frontend
npm test
# or
yarn test
```

## 📦 Production Build

### Backend

Build the optimized release binary:

```bash
cd backend
cargo build --release
```

The binary will be available at `target/release/backend`.

### Frontend

Build the production-ready frontend:

```bash
cd frontend
npm run build
# or
yarn build
```

Start the production server:

```bash
npm start
# or
yarn start
```

## 🚢 Deployment

### Docker Deployment (Recommended)

Create a `docker-compose.yml` in the project root:

```yaml
version: '3.8'

services:
  postgres:
    image: postgres:16
    environment:
      POSTGRES_USER: musicuser
      POSTGRES_PASSWORD: musicpass
      POSTGRES_DB: music
    volumes:
      - postgres_data:/var/lib/postgresql/data
    ports:
      - "5432:5432"

  backend:
    build: ./backend
    depends_on:
      - postgres
    environment:
      DATABASE_URL: postgresql://musicuser:musicpass@postgres:5432/music
      JWT_SECRET_KEY: ${JWT_SECRET_KEY}
    ports:
      - "8000:8000"

  frontend:
    build: ./frontend
    depends_on:
      - backend
    environment:
      API_BASE_URL: http://backend:8000/api
    ports:
      - "3000:3000"

volumes:
  postgres_data:
```

Deploy with:

```bash
docker-compose up -d
```

### Cloud Deployment Options

- **Backend:** AWS EC2, DigitalOcean, Heroku, Railway
- **Frontend:** Vercel, Netlify, AWS Amplify
- **Database:** AWS RDS, DigitalOcean Managed Databases, Supabase

## 🔐 Security Considerations

- All passwords are hashed using **Argon2**
- JWT tokens for secure authentication
- HTTPS/TLS encryption for data in transit
- SQL injection protection via SQLx prepared statements
- CORS configuration for API security
- Environment variables for sensitive data

## 📝 License

This project is licensed under the MIT License. See the [LICENSE](./LICENSE) file for details.

## 🙏 Acknowledgments

- [Axum](https://github.com/tokio-rs/axum) - Web framework
- [Next.js](https://nextjs.org/) - React framework
- [ShadCN](https://ui.shadcn.com/) - UI components
- [SQLx](https://github.com/launchbadge/sqlx) - Database toolkit
- [Symphonia](https://github.com/pdeljanov/Symphonia) - Audio decoding

## 📧 Contact

For questions or support, please open an issue on GitHub.

---

**Happy coding! 🎧🚀**
