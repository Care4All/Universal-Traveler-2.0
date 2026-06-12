# Universal Traveler ♿

**Comprehensive Accessibility Navigation Platform**

AccessLink helps users with mobility challenges navigate physical environments safely. It provides real-time accessibility scoring, color-coded venue markers, and personalized navigation guidance based on each user's specific equipment and endurance needs.

## Project Structure

```
AccessLink/
├── backend/     # Node.js/Express/MongoDB API server
├── mobile/      # React Native (Expo) iOS/Android app
├── web/         # React web application
└── DEPLOYMENT.md
```

## Features

- **Personalized Accessibility Profiles** — Store DME type, equipment width, endurance limits, elevator requirements
- **Accessibility Scoring Engine** — Doorway fit check, endurance assessment, ramp safety (ADA 1:12 ratio), surface energy calculations
- **Color-Coded Venue Markers** — 🟢 Green (safe), 🟠 Orange (caution), 🔴 Red (not recommended)
- **50+ Mock Locations** — Realistic venues across NYC, LA, Chicago, Boston, and Seattle
- **JWT Authentication** — Secure login/signup with bcryptjs password hashing
- **Favorites Management** — Bookmark accessible locations across all platforms
- **Offline Support** — Mobile app caches location data via AsyncStorage

## Quick Start

### Prerequisites
- Node.js 18+
- MongoDB (local or Atlas)
- Expo CLI (for mobile development)

### 1. Backend

```bash
cd backend
cp .env.example .env          # Configure MongoDB URI and JWT secret
npm install
npm run seed                  # Seed 55 mock locations
npm run dev                   # Start on http://localhost:3000
```

### 2. Web App

```bash
cd web
cp .env.example .env          # Set VITE_API_URL
npm install
npm run dev                   # Start on http://localhost:5173
```

### 3. Mobile App

```bash
cd mobile
cp .env.example .env          # Set EXPO_PUBLIC_API_URL
npm install
npx expo start                # Start Expo development server
```

Scan the QR code with Expo Go on your device, or press `i` for iOS simulator / `a` for Android emulator.

## API Endpoints

| Method | Endpoint | Description | Auth |
|--------|----------|-------------|------|
| POST | `/api/auth/signup` | Create account | — |
| POST | `/api/auth/login` | Login, receive JWT | — |
| GET | `/api/auth/me` | Get current user | ✅ |
| PUT | `/api/auth/profile` | Update profile | ✅ |
| GET | `/api/locations` | List locations (filterable) | — |
| GET | `/api/locations/:id` | Get location details | — |
| POST | `/api/audits` | Run full accessibility audit | ✅ |
| POST | `/api/audits/endurance` | Endurance/energy assessment | ✅ |
| POST | `/api/audits/ramp-safety` | Ramp safety evaluation | ✅ |
| GET | `/api/audits/history` | User audit history | ✅ |
| GET | `/api/favorites` | Get user favorites | ✅ |
| POST | `/api/favorites` | Add location to favorites | ✅ |
| DELETE | `/api/favorites/:locationId` | Remove from favorites | ✅ |

## Accessibility Scoring

| Check | Criteria | Score Impact |
|-------|----------|-------------|
| Doorway Clearance | `doorWidth >= equipmentWidth + 2"` | −40 if fails |
| Endurance | `walkingDistance <= userLimit` | −30 if fails |
| Elevator | Required by user but missing | −20 |
| Ramp Safety | Slope ≤ 4.8° (ADA 1:12) | −20 if fails |

**Score ≥ 80** → 🟢 Green &nbsp;|&nbsp; **Score 60–79** → 🟠 Orange &nbsp;|&nbsp; **Score < 60** → 🔴 Red

## Surface Energy Multipliers

| Surface | Multiplier |
|---------|-----------|
| Concrete/Asphalt | 1.0× |
| Tile/Wood | 1.1× |
| Carpet | 1.3× |
| Cobblestone | 1.8× |
| Gravel | 2.0× |

## Technology Stack

| Layer | Technologies |
|-------|-------------|
| Backend | Node.js, Express, MongoDB, Mongoose, JWT, bcryptjs |
| Mobile | React Native, Expo, React Navigation v6, react-native-maps, AsyncStorage |
| Web | React 18, TypeScript, React Router v6, Vite, Leaflet |
| Database | MongoDB (Atlas or local) |

## License

MIT — See [LICENSE](LICENSE)
