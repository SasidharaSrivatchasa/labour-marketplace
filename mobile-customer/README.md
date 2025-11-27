mobile-customer/README.md  # Labour Marketplace - Customer Mobile App

React Native Expo app for customers to find and book labour services.

## Features

- **Service Discovery**: Browse available services by category and location
- **Real-time Geolocation**: Find nearby service providers
- **Booking Management**: Create, track, and manage service bookings
- **Payment Integration**: Stripe and Razorpay payment methods
- **Rating System**: Rate and review service providers
- **Wallet**: In-app wallet for balance management
- **Multi-language Support**: Support for 6 Indian languages
- **Push Notifications**: Real-time booking updates
- **Chat**: Direct messaging with service providers

## Tech Stack

- React Native with Expo
- TypeScript
- Redux Toolkit (State Management)
- Socket.io (Real-time communication)
- Google Maps API
- Firebase Cloud Messaging

## Project Structure

```
mobile-customer/
├── src/
│   ├── screens/
│   │   ├── AuthScreen.tsx
│   │   ├── HomeScreen.tsx
│   │   ├── BrowseScreen.tsx
│   │   ├── BookingScreen.tsx
│   │   └── ProfileScreen.tsx
│   ├── components/
│   │   ├── ServiceCard.tsx
│   │   ├── BookingCard.tsx
│   │   └── LocationPicker.tsx
│   ├── navigation/
│   │   └── Navigation.tsx
│   ├── store/
│   │   ├── bookingSlice.ts
│   │   ├── authSlice.ts
│   │   └── store.ts
│   ├── services/
│   │   ├── apiClient.ts
│   │   ├── authService.ts
│   │   └── bookingService.ts
│   ├── locales/
│   │   ├── en.json
│   │   ├── hi.json
│   │   └── ...
│   └── App.tsx
├── assets/
├── package.json
├── app.json
└── eas.json
```

## Getting Started

1. Install dependencies:
```bash
npm install
```

2. Start Expo:
```bash
npm start
```

3. Scan QR code with Expo Go app

## API Integration

Connects to the backend API at `http://localhost:3000/api`

## Authentication

- OTP-based authentication
- JWT tokens for secure API calls
- Refresh token mechanism

## Build & Deploy

```bash
# Build for iOS
eas build --platform ios

# Build for Android
eas build --platform android
```
