# Labour Marketplace

[![GitHub](https://img.shields.io/badge/GitHub-labour--marketplace-181717?logo=github)](https://github.com/SasidharaSrivatchasa/labour-marketplace)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](./LICENSE)
[![Node.js](https://img.shields.io/badge/Node.js-18+-green)](https://nodejs.org/)
[![React Native](https://img.shields.io/badge/React%20Native-0.73-blue)](https://reactnative.dev/)

A **production-ready on-demand labour marketplace platform** serving daily-wage and contract labour across India.

## 📋 Table of Contents

- [Features](#features)
- [Architecture](#architecture)
- [Tech Stack](#tech-stack)
- [Quick Start](#quick-start)
- [Project Structure](#project-structure)
- [API Endpoints](#api-endpoints)
- [Database](#database)
- [Deployment](#deployment)
- [Contributing](#contributing)
- [License](#license)

## ✨ Features

### 🛍️ Customer App
- ✅ OTP-based authentication (5-minute expiry)
- ✅ Browse and book services (Repair/Contract)
- ✅ Real-time provider tracking with QR verification
- ✅ Multi-language support (English, Telugu, Hindi, Kannada, Tamil, Malayalam)
- ✅ Payment integration & wallet management
- ✅ Booking history & ratings
- ✅ Push notifications

### 👷 Provider App
- ✅ KYC verification with Aadhaar/ID upload
- ✅ Online/Offline toggle with geolocation
- ✅ Job request notifications (3-minute accept window)
- ✅ QR scanner for job verification
- ✅ Real-time turn-by-turn navigation
- ✅ Earnings dashboard & withdrawals
- ✅ Bank account management

### 🖥️ Admin Dashboard
- ✅ Real-time booking management
- ✅ Provider & customer management
- ✅ KYC document verification
- ✅ Wallet & payment settlements
- ✅ Dispute resolution
- ✅ Analytics & reporting
- ✅ Commission tracking

## 🏗️ Architecture

```
Clients (Mobile Apps) → API Gateway (Rate Limiting)
                    ↓
        Backend Services (Node.js + TypeScript)
                    ↓
    PostgreSQL (PostGIS) ← → Redis Cache
                    ↓
    Payment Gateway (Razorpay/Stripe)
    Firebase (Push Notifications)
    Google Maps (Geolocation)
```

### Key Components
- **Backend**: Node.js + Express + TypeScript
- **Database**: PostgreSQL 12+ with PostGIS
- **Cache**: Redis for sessions and rate limiting
- **Queue**: Bull for background jobs
- **Authentication**: OTP + JWT with refresh tokens
- **Payments**: Razorpay/Stripe integration
- **Notifications**: Firebase FCM
- **Geolocation**: Google Maps API

## 💻 Tech Stack

### Backend
```
- Runtime: Node.js 18+
- Language: TypeScript
- Framework: Express.js
- Database: PostgreSQL 12+ with PostGIS
- Cache: Redis
- Job Queue: Bull
- Auth: JWT + OTP
- Payments: Razorpay/Stripe
- Notifications: Firebase FCM
```

### Mobile Apps
```
- Framework: React Native (Expo)
- Navigation: React Navigation
- State: Context API / Zustand
- HTTP: Axios
- Localization: i18next
- Maps: Google Maps / React Native Maps
```

### Admin Dashboard
```
- Framework: React 18+
- Routing: React Router v6
- HTTP: Axios
- UI: Material-UI / Ant Design
- Charts: Recharts
- Styling: Tailwind CSS
```

## 🚀 Quick Start

### Prerequisites
- Node.js 18+
- Docker & Docker Compose (optional)
- PostgreSQL 12+
- Redis 6+
- Git

### Backend Setup

```bash
git clone https://github.com/SasidharaSrivatchasa/labour-marketplace.git
cd labour-marketplace/backend

npm install
cp .env.example .env
# Edit .env with your configuration

# Option 1: With Docker
docker-compose up -d

# Option 2: Manual
npm run dev
```

Backend will be available at: `http://localhost:3000`

### Customer App Setup

```bash
cd labour-marketplace/mobile-customer
npm install
cp .env.example .env.local
npx expo start

# Scan QR with Expo Go on your phone
```

### Provider App Setup

```bash
cd labour-marketplace/mobile-provider
npm install
cp .env.example .env.local
npx expo start
```

### Admin Dashboard Setup

```bash
cd labour-marketplace/admin-dashboard
npm install
cp .env.example .env.local
npm start
```

## 📁 Project Structure

```
labour-marketplace/
├── backend/                 # Node.js + TypeScript backend
│   ├── src/
│   │   ├── controllers/    # Request handlers
│   │   ├── services/       # Business logic
│   │   ├── routes/         # API routes
│   │   ├── middlewares/    # Custom middleware
│   │   ├── models/         # Data models
│   │   ├── utils/          # Utilities
│   │   ├── types/          # TypeScript types
│   │   └── adapters/       # External integrations
│   ├── tests/              # Test files
│   ├── migrations/         # Database migrations
│   ├── package.json
│   ├── Dockerfile
│   └── docker-compose.yml
│
├── mobile-customer/         # React Native customer app
│   ├── src/
│   │   ├── screens/        # Screen components
│   │   ├── components/     # Reusable components
│   │   ├── navigation/     # Navigation setup
│   │   ├── services/       # API services
│   │   ├── context/        # React contexts
│   │   ├── hooks/          # Custom hooks
│   │   └── utils/          # Utilities
│   ├── app.json
│   └── package.json
│
├── mobile-provider/         # React Native provider app
│   ├── src/
│   ├── app.json
│   └── package.json
│
├── admin-dashboard/         # React admin web app
│   ├── src/
│   │   ├── pages/          # Page components
│   │   ├── components/     # Reusable components
│   │   ├── services/       # API services
│   │   └── utils/          # Utilities
│   ├── public/
│   └── package.json
│
├── database/                # Database schemas
│   ├── postgresql_schema.sql
│   ├── mongodb_schema.js
│   └── seeds.sql
│
├── docs/                    # Documentation
│   ├── ARCHITECTURE.md
│   ├── API_DOCUMENTATION.md
│   ├── DATABASE_DESIGN.md
│   ├── DEPLOYMENT_GUIDE.md
│   └── DEVELOPMENT_SETUP.md
│
├── .gitignore
├── .env.example
├── README.md               # This file
├── CONTRIBUTING.md
└── LICENSE
```

## 📚 API Endpoints

### Authentication
```
POST   /api/v1/auth/signup           - Register user
POST   /api/v1/auth/login-otp        - Request OTP
POST   /api/v1/auth/verify-otp       - Verify OTP & login
POST   /api/v1/auth/refresh          - Refresh access token
```

### Bookings
```
POST   /api/v1/bookings              - Create booking
GET    /api/v1/bookings/:id          - Get booking details
POST   /api/v1/bookings/:id/accept   - Provider accepts job
POST   /api/v1/bookings/:id/start    - Start job via QR
POST   /api/v1/bookings/:id/end      - End job
POST   /api/v1/bookings/:id/payment  - Process payment
```

### Providers
```
POST   /api/v1/providers/register    - Register as provider
GET    /api/v1/providers/:id         - Get provider profile
POST   /api/v1/providers/:id/availability - Update availability
GET    /api/v1/providers/available   - List available providers
```

### Wallet
```
GET    /api/v1/wallets/:providerId   - Get wallet balance
POST   /api/v1/wallets/:providerId/withdraw - Request withdrawal
```

### Admin
```
GET    /api/v1/admin/bookings        - List all bookings
GET    /api/v1/admin/providers       - List all providers
POST   /api/v1/admin/assign          - Override provider assignment
```

See [API_DOCUMENTATION.md](./docs/API_DOCUMENTATION.md) for detailed endpoint documentation.

## 🗄️ Database

### PostgreSQL Tables
- `users` - Customer and provider users
- `providers` - Provider profiles with geolocation
- `services` - Available services and categories
- `bookings` - Booking records with lifecycle
- `wallets` - Provider wallet balances
- `transactions` - Payment and wallet transactions
- `ratings` - Service ratings and reviews
- `disputes` - Dispute resolution tracking
- `kyc_documents` - KYC verification documents

See [DATABASE_DESIGN.md](./docs/DATABASE_DESIGN.md) for detailed schema.

## 🚢 Deployment

### Docker Deployment

```bash
# Build backend image
docker build -t labour-marketplace-backend ./backend

# Run with docker-compose
docker-compose up -d
```

### Production Checklist
- [ ] Change all default secrets in .env
- [ ] Enable HTTPS/TLS
- [ ] Setup firewall rules
- [ ] Enable database backups
- [ ] Configure CORS properly
- [ ] Setup rate limiting
- [ ] Enable audit logging
- [ ] Configure monitoring & alerts
- [ ] Setup CI/CD pipeline
- [ ] Regular security updates

See [DEPLOYMENT_GUIDE.md](./docs/DEPLOYMENT_GUIDE.md) for detailed deployment instructions.

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/amazing-feature`
3. Commit changes: `git commit -m '[feat] Add amazing feature'`
4. Push to branch: `git push origin feature/amazing-feature`
5. Open a Pull Request

See [CONTRIBUTING.md](./CONTRIBUTING.md) for detailed guidelines.

## 📝 Documentation

- [Architecture Design](./docs/ARCHITECTURE.md)
- [API Documentation](./docs/API_DOCUMENTATION.md)
- [Database Design](./docs/DATABASE_DESIGN.md)
- [Deployment Guide](./docs/DEPLOYMENT_GUIDE.md)
- [Development Setup](./docs/DEVELOPMENT_SETUP.md)

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](./LICENSE) file for details.

## 👨‍💻 Author

**Sasidhara Srivatchasa**
- GitHub: [@SasidharaSrivatchasa](https://github.com/SasidharaSrivatchasa)
- Email: sasidhara.srivatchasa@example.com

## 🙏 Acknowledgments

- Built with ❤️ for India's labour marketplace
- Supports 6 Indian languages
- Production-ready at scale

---

**Last Updated**: November 27, 2025  
**Version**: 1.0.0  
**Status**: ✅ Production Ready
