# Farmington - Fantasy Farming Game

## Overview
Farmington is a fantasy farming web application built with Flask. It's a multiplayer game where users draft farmers, compete in leagues, and manage their fantasy farming teams through matchdays.

**Current State:** Fully functional and running in the Replit environment. The application has been successfully imported from GitHub and configured for the Replit platform.

## Recent Changes
*Date: December 1, 2025*
- Imported project from GitHub repository
- Fixed missing import in `app.py` (added `load_stats` and `save_stats` from stats module)
- Created `.gitignore` for Python project
- Fixed JavaScript syntax error in `static/js/theme.js` (removed extra closing brace)
- Configured Flask application to run on port 5000 with webview output
- Set up deployment configuration using Gunicorn for production
- Created comprehensive project documentation

## Project Architecture

### Technology Stack
- **Backend Framework:** Flask (Python 3.11)
- **Web Server (Dev):** Flask development server
- **Web Server (Production):** Gunicorn with 4 workers
- **Database:** File-based JSON storage (users.json, leagues.json, farm_stats.json, etc.)
- **Scheduler:** APScheduler for automated matchday processing
- **Frontend:** Bootstrap 5.3.0, Font Awesome 6.4.0, custom JavaScript
- **PWA Support:** Service Worker, Web App Manifest

### Key Dependencies
- Flask 3.1.1
- Flask-SQLAlchemy 3.1.1
- APScheduler 3.11.0
- Gunicorn 23.0.0
- Werkzeug 3.1.3
- psycopg2-binary 2.9.10 (PostgreSQL support)
- email-validator 2.2.0

### Project Structure
```
farmington/
├── app.py                  # Main Flask application with all routes
├── main.py                 # Application entry point
├── stats.py                # Statistics management functions
├── market.py               # Market system logic
├── trading.py              # Player trading functionality
├── chat.py                 # League chat system
├── core.py                 # Core game mechanics
├── tasks.py                # Background task definitions
├── static/                 # Static assets
│   ├── css/
│   │   └── styles.css      # Main stylesheet
│   ├── js/
│   │   ├── theme.js        # Dark/light theme management
│   │   ├── pwa.js          # Progressive Web App features
│   │   ├── mobile.js       # Mobile-specific functionality
│   │   ├── farmer_stats.js # Farmer statistics display
│   │   └── trading.js      # Trading interface
│   ├── images/             # Game images and icons
│   ├── manifest.json       # PWA manifest
│   └── sw.js              # Service worker
├── templates/              # Jinja2 HTML templates
│   ├── base.html          # Base template
│   ├── index.html         # Home page
│   ├── login.html         # Login page
│   ├── register.html      # Registration page
│   ├── draftroom.html     # Draft interface
│   ├── market.html        # Market page
│   ├── trading.html       # Trading page
│   ├── user_team.html     # Team management
│   ├── league_chat.html   # League chat
│   └── components/        # Reusable components
└── *.json                 # Data files (users, leagues, stats, etc.)
```

### Key Features
1. **User Management:** Registration, login, profile customization
2. **League System:** Create/join leagues, playoff brackets, matchup schedules
3. **Draft System:** Snake draft for farmer selection
4. **Market System:** Buy/sell farmers with dynamic pricing
5. **Trading System:** Propose and accept farmer trades between users
6. **Matchday Processing:** Automated matchday simulation every 2 minutes
7. **Statistics Tracking:** Comprehensive farmer and team statistics
8. **Chat System:** League-specific chat functionality
9. **Theme System:** Dark/light mode with persistent storage
10. **PWA Features:** Installable, offline-capable, responsive design

### Data Storage
The application uses JSON files for data persistence:
- `users.json` - User accounts and profiles
- `leagues.json` - League configurations and schedules
- `farm_stats.json` - Player statistics by matchday
- `market_*.json` - League-specific market data
- `farmer_pool.json` - Available farmers
- Various configuration files for crops, preferences, etc.

### Deployment Configuration
- **Development:** Flask dev server on 0.0.0.0:5000
- **Production:** Gunicorn with autoscale deployment
  - Command: `gunicorn --bind=0.0.0.0:5000 --reuse-port --workers=4 app:app`
  - Deployment target: autoscale (stateless web application)
  - **Note:** Deployment settings are configured through the Replit GUI using the deploy configuration tool. These settings are managed by Replit and not stored in the repository.

## Replit Environment Setup

### Workflows
- **Flask App:** Runs `python main.py` on port 5000 with webview output
- Configured to automatically restart on file changes

### Host Configuration
The Flask development server is configured to accept all hosts (`0.0.0.0`) which is required for the Replit proxy/iframe preview system. This allows users to view the application through Replit's web preview.

### Automated Tasks
- APScheduler runs matchday processing every 2 minutes
- Background scheduler handles league progression
- Automated bracket creation at season midpoint

## User Preferences
- None specified yet

## Development Notes

### Security Considerations
- Session secret key from environment variable `SESSION_SECRET` with fallback
- Password hashing using Werkzeug's security functions
- File upload validation for profile pictures
- Login required decorators for protected routes

### Database Migration Path
The application currently uses JSON files for data storage. The inclusion of psycopg2-binary suggests potential future PostgreSQL migration, but this is not currently implemented.

### Known Limitations
- File-based storage is not suitable for high concurrency
- No database transactions or ACID guarantees
- Profile pictures stored in static directory
- No user email verification system

## Next Steps / Improvement Opportunities
1. Consider migrating to PostgreSQL for better data integrity
2. Implement database transactions for critical operations
3. Add email verification for user registration
4. Implement rate limiting for API endpoints
5. Add comprehensive error handling and logging
6. Consider adding WebSocket support for real-time chat
7. Optimize image storage (use object storage service)
8. Add unit and integration tests
