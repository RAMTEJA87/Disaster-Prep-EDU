#Disaster Prep EDU  – Complete Disaster Preparedness Education Platform

[![React](https://img.shields.io/badge/React-18.3.1-blue.svg)](https://reactjs.org/)
[![Node.js](https://img.shields.io/badge/Node.js-Express-green.svg)](https://nodejs.org/)
[![MongoDB](https://img.shields.io/badge/Database-MongoDB-brightgreen.svg)](https://mongodb.com/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

A comprehensive, gamified educational platform that teaches disaster preparedness to children aged 10-15 through interactive learning, games, quizzes, and community engagement.

## 🎯 **Key Features**

### 📚 **Educational Content**
- **80+ Quiz Questions** across 8 disaster types with expert-crafted scenarios
- **8 Virtual Drills** with step-by-step emergency procedures
- **Interactive Learning Modules** covering natural and man-made disasters
- **Real-time Weather Alerts** with location-based safety recommendations

### 🎮 **Gamification System**
- **6 Interactive Games** with scenario-based decision making
- **Complete Points & Badges System** with 10+ achievement types
- **Student Leaderboards** with competitive rankings
- **Progress Tracking** with levels and streaks
- **Sound Effects & Animations** for engaging user experience

### 👥 **Community & Communication**
- **Multi-channel Community System** (General, Announcements, Help, Study Groups)
- **Role-based Access Control** (Students vs Teachers/Administrators)
- **Real-time Messaging** with localStorage persistence
- **AI Chatbot Assistant** for instant help and guidance

### 🏫 **Teacher Administration**
- **Comprehensive Teacher Dashboard** with student analytics
- **Student Management System** with progress monitoring
- **Performance Analytics** by disaster type and individual progress
- **Account Management** with secure deletion capabilities

### 📱 **Modern UI/UX**
- **Mobile-First Responsive Design** optimized for all devices
- **Vibrant, Kid-Friendly Interface** with 50+ CSS animations
- **Accessibility Features** with ARIA labels and keyboard navigation
- **Dark/Light Theme Support** with smooth transitions

## 🛠️ **Technology Stack**

### **Frontend**
- **React 18.3.1** with Vite for fast development
- **React Router DOM** for seamless navigation
- **Axios** for API communication
- **Context API** for state management
- **CSS3** with advanced animations and responsive design

### **Backend**
- **Node.js** with Express.js framework
- **MongoDB** with Mongoose ODM
- **JWT Authentication** for secure user sessions
- **bcryptjs** for password hashing
- **CORS & Helmet** for security
- **Rate Limiting** for API protection

### **Development Tools**
- **Vite** for fast build and hot reload
- **Nodemon** for backend development
- **ESLint** for code quality
- **Git** for version control

## Project Structure
```
sih/
  backend/
    src/
      index.js
      app.js
      utils/db.js
      middleware/auth.js
      models/{User,LearningModule,QuizResult,DrillLog}.js
      routes/{index,auth,modules,quizzes,progress,weather,chatbot}.js
    scripts/seed.js
    .env.example
    package.json
  frontend/
    src/
      components/{Navbar,WeatherWidget,ChatbotBuddy,ProgressBar,Badge}.jsx
      context/AuthContext.jsx
      pages/{Home,Modules,ModuleDetail,Drill,Dashboard,Avatar,Leaderboard,Login,Register}.jsx
      routes/ProtectedRoute.jsx
      styles/global.css
      App.jsx
      main.jsx
    index.html
    .env.example
    package.json
  README.md
```

## Prerequisites
- Node.js 18+
- MongoDB running locally (or provide a connection string)
- OpenWeatherMap API key (free tier works for current weather and geocoding)

## Backend Setup
1. Copy environment file and edit values:
   ```bash
   cp backend/.env.example backend/.env
   ```
   - `MONGO_URI` can be left as default for local MongoDB.
   - Set `JWT_SECRET` to a strong secret.
   - Set `OPENWEATHER_API_KEY` to your key from https://openweathermap.org/api
   - Optionally update `CORS_ORIGINS` (default `http://localhost:5173`).

2. Install dependencies and seed demo data:
   ```bash
   cd backend
   npm install
   npm run seed
   npm run dev
   ```
   The API will run at `http://localhost:5000`.

3. Demo accounts created by seeding:
   - Student: `sam@safecampus.local` / `password123`
   - Admin: `admin@safecampus.local` / `password123`

## Frontend Setup
1. Copy env file (the default points to backend on port 5000):
   ```bash
   cp frontend/.env.example frontend/.env
   ```
2. Install and run:
   ```bash
   cd frontend
   npm install
   npm run dev
   ```
   The app will run at `http://localhost:5173`.

## Usage Guide
- Open the app, visit `Modules` to read a module and take its quiz.
- Login with the demo student credentials to submit quiz answers and earn badges.
- Try the `Virtual Drill` page to run a timed drill and save the result.
- Check `Dashboard` for progress, badges, and quiz results.
- Customize your avatar on the `Avatar` page.
- See the `Leaderboard` for top total scores.
- Use the bottom-right chat bubble to ask Jr. SafeBot safety questions.
- The bottom-left `Weather` widget shows current weather; if alerts exist for your city, a red alert bar appears.

## API Endpoints (Summary)
- `POST /api/auth/register` – Create user, returns JWT
- `POST /api/auth/login` – Login, returns JWT
- `GET /api/modules` – List modules
- `GET /api/modules/:id` – Module details
- `POST /api/modules` – Create module (admin)
- `PUT /api/modules/:id` – Update module (admin)
- `DELETE /api/modules/:id` – Delete module (admin)
- `POST /api/quizzes/:moduleId/submit` – Submit quiz (auth)
- `GET /api/quizzes/my` – My quiz results (auth)
- `GET /api/quizzes/leaderboard` – Top users by score
- `GET /api/progress/me` – My profile/progress (auth)
- `PUT /api/progress/avatar` – Update avatar (auth)
- `POST /api/progress/drills` – Save drill log (auth)
- `GET /api/progress/drills/my` – My drill logs (auth)
- `GET /api/weather/current?city=City` – Current weather via OWM proxy
- `GET /api/weather/alerts?city=City` – Alerts via One Call (falls back gracefully)
- `POST /api/chatbot/ask` – Jr. SafeBot mock response

## Accessibility Notes
- Alt text on images and ARIA labels on key widgets.
- Keyboard-accessible buttons and focus outlines enabled by default CSS.

## Seeding and Sample Content
- `scripts/seed.js` inserts:
  - 2 users (admin/user) with demo credentials
  - 3 modules with age-appropriate quiz questions

## Visual Mockups (Descriptions)
- Home banner: Gradient blue→green with a bright yellow CTA button.
- Module cards: Rounded white cards with playful placeholder images per disaster type.
- Weather widget: Small white card fixed at bottom-left with city dropdown. Red alert bar appears when alerts exist.
- Chatbot: Floating chat button bottom-right; opening reveals friendly chat box with speech bubbles.
- Dashboard: Avatar, total score, progress bar, badges, and recent quiz results in a card grid.

## Notes
- For production, consider HTTPS, secure cookie storage for JWT/refresh tokens, stricter CORS, and more granular rate limiting.
- The chatbot is a mock; you can integrate a real AI provider behind `/api/chatbot/ask`.
