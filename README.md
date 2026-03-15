# Kalornik (Prosty Deficyt)

A personal web application for calorie tracking, designed with simplicity and motivation in mind through a streak and reward system. Built as an MVP with a mobile-first responsive interface optimized for quick thumb-based interactions.

## Table of Contents

- [Project Description](#project-description)
- [Tech Stack](#tech-stack)
- [Getting Started Locally](#getting-started-locally)
- [Available Scripts](#available-scripts)
- [Project Scope](#project-scope)
- [Project Status](#project-status)
- [License](#license)

## Project Description

Kalornik addresses the common problem of calorie counting being boring and easily abandoned. The app introduces gamification elements (streak counter, virtual shields) combined with a simplified interface to encourage consistent daily usage.

### Key Features

- **Plan Generator** - Calculate your daily calorie limit based on personal data using the Mifflin-St Jeor formula
- **Streak Counter** - Track consecutive days of maintaining your diet to stay motivated
- **Virtual Shields** - Earn rewards for consistency that protect your streak on difficult days
- **Favorite Meals** - Quick one-click logging of your regular meals and recipes
- **Charts & Reports** - Weekly and monthly summaries of your progress and weight trends
- **Cloud Sync** - Your data is secure and accessible from any device

### Core Characteristics

- Web application with responsive mobile-optimized design
- Backend powered by Supabase for authentication and data storage
- Cloud-synchronized data accessible from any device
- Polish language interface with Polish product database
- Completely free application

## Tech Stack

### Frontend

- **Astro 5** - Fast, efficient pages and applications with minimal JavaScript
- **React 19** - Interactive components where needed
- **TypeScript 5** - Static typing for better code quality and IDE support
- **Tailwind CSS 4** - Utility-first styling
- **shadcn/ui** - Accessible React component library

### Backend

- **Supabase** - Complete backend solution including:
  - PostgreSQL database
  - Built-in user authentication
  - Backend-as-a-Service SDK

### AI Integration

- **Openrouter.ai** - Access to various AI models (OpenAI, Anthropic, Google)

### CI/CD & Hosting

- **GitHub Actions** - CI/CD pipelines
- **DigitalOcean / Cloudflare** - Docker-based hosting

## Getting Started Locally

### Prerequisites

- Node.js 22.14.0 (use [nvm](https://github.com/nvm-sh/nvm) for version management)
- npm or yarn

### Installation

1. Clone the repository:

   ```bash
   git clone https://github.com/your-username/kalornik.git
   cd kalornik
   ```

2. Install the correct Node.js version:

   ```bash
   nvm use
   ```

3. Install dependencies:

   ```bash
   npm install
   ```

4. Start the development server:

   ```bash
   npm run dev
   ```

5. Open your browser and navigate to `http://localhost:4321`

## Available Scripts

| Script            | Description                          |
| ----------------- | ------------------------------------ |
| `npm run dev`     | Start the development server         |
| `npm run build`   | Build the application for production |
| `npm run preview` | Preview the production build locally |
| `npm run lint`    | Run ESLint to check for code issues  |
| `npm run lint:fix`| Run ESLint and automatically fix issues |
| `npm run format`  | Format code with Prettier            |
| `npm run astro`   | Run Astro CLI commands               |

## Project Scope

### In Scope (MVP)

- Email/password authentication via Supabase
- Calorie calculation using Mifflin-St Jeor formula
- Manual product entry with flexible unit system (g, ml, pieces, portions)
- Basic Polish product database (200-500 items)
- Custom product creation
- Favorite meals/recipes for quick logging
- Streak tracking with 10% tolerance
- Shield reward system (earn 1 shield per 7-day streak, max 3)
- Daily weight tracking with visual reminder
- Charts (daily calories vs limit, weight trend)
- Key statistics display
- 7-day edit window for entries
- Responsive mobile web interface
- Data export (JSON/CSV)

### Out of Scope (MVP)

- Barcode scanner
- AI-powered features (image analysis, suggestions)
- Social features (friends, leaderboards)
- Push notifications
- Offline mode
- Native mobile applications (iOS/Android)
- Integration with fitness devices
- Detailed macronutrient tracking display

## Project Status

**Current Phase:** MVP Development

The project is in active development. Core features are being implemented according to the product requirements document.

### Success Criteria

- Application loads in under 3 seconds on 4G connection
- Interface is fully responsive on all phone screen sizes (320px to 428px)
- User can add a favorite meal in under 5 seconds
- Streak and shield calculations are 100% accurate

## License

This project is private and not licensed for public use.
