# The Gaadi - Full Stack Application

A full-stack web application with a Next.js frontend and Node.js backend with PostgreSQL database.

## Project Structure

```
the-gaadi/
├── frontend/          # Next.js frontend application
├── backend/           # Node.js backend API
└── README.md         # This file
```

## Features

- **Frontend**: Beautiful "Good Morning" page with a form to collect user information
- **Backend**: RESTful API with Express.js
- **Database**: PostgreSQL for data persistence
- **Form Fields**: Name, Phone Number, and Email Address

## Prerequisites

Before running this application, make sure you have the following installed:

- **Node.js** (v16 or higher)
- **PostgreSQL** (v12 or higher)
- **npm** (comes with Node.js)

## Setup Instructions

### 1. Database Setup

1. **Install PostgreSQL** (if not already installed):
   ```bash
   # Ubuntu/Debian
   sudo apt update
   sudo apt install postgresql postgresql-contrib
   
   # macOS (with Homebrew)
   brew install postgresql
   
   # Windows
   # Download from https://www.postgresql.org/download/windows/
   ```

2. **Start PostgreSQL service**:
   ```bash
   # Ubuntu/Debian
   sudo systemctl start postgresql
   
   # macOS
   brew services start postgresql
   ```

3. **Create database and user**:
   ```bash
   # Connect to PostgreSQL as superuser
   sudo -u postgres psql
   
   # Create database
   CREATE DATABASE thegaadi;
   
   # Create user (optional, or use default postgres user)
   CREATE USER gaadi_user WITH PASSWORD 'your_password';
   GRANT ALL PRIVILEGES ON DATABASE thegaadi TO gaadi_user;
   
   # Exit PostgreSQL
   \q
   ```

4. **Initialize database schema**:
   ```bash
   cd backend
   node database/init.js
   ```

### 2. Backend Setup

1. **Navigate to backend directory**:
   ```bash
   cd backend
   ```

2. **Install dependencies**:
   ```bash
   npm install
   ```

3. **Configure environment variables**:
   Edit the `.env` file in the backend directory with your database credentials:
   ```env
   DB_HOST=localhost
   DB_PORT=5432
   DB_NAME=thegaadi
   DB_USER=postgres
   DB_PASSWORD=your_password
   PORT=5000
   ```

4. **Build and run the backend**:
   ```bash
   # Development mode (with auto-reload)
   npm run dev
   
   # Or production mode
   npm run build
   npm start
   ```

   The backend will be available at `http://localhost:5000`

### 3. Frontend Setup

1. **Navigate to frontend directory**:
   ```bash
   cd frontend
   ```

2. **Install dependencies**:
   ```bash
   npm install
   ```

3. **Run the development server**:
   ```bash
   npm run dev
   ```

   The frontend will be available at `http://localhost:3000`

## Usage

1. Open your browser and go to `http://localhost:3000`
2. You'll see a beautiful "Good Morning" page with a form
3. Fill in your name, phone number, and email address
4. Click the "Submit" button
5. Your data will be saved to the PostgreSQL database

## API Endpoints

### Backend API (http://localhost:5000)

- `GET /` - Health check endpoint
- `POST /api/users` - Create a new user
- `GET /api/users` - Get all users

### Example API Usage

**Create a user**:
```bash
curl -X POST http://localhost:5000/api/users \
  -H "Content-Type: application/json" \
  -d '{
    "name": "John Doe",
    "phone": "+1234567890",
    "email": "john@example.com"
  }'
```

**Get all users**:
```bash
curl http://localhost:5000/api/users
```

## Database Schema

The `users` table has the following structure:

```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    phone VARCHAR(20) NOT NULL,
    email VARCHAR(255) UNIQUE NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

## Troubleshooting

### Common Issues

1. **Database connection error**:
   - Make sure PostgreSQL is running
   - Check your database credentials in the `.env` file
   - Ensure the database `thegaadi` exists

2. **Port already in use**:
   - Change the PORT in the `.env` file
   - Kill the process using the port: `lsof -ti:5000 | xargs kill -9`

3. **Frontend can't connect to backend**:
   - Make sure the backend is running on port 5000
   - Check if CORS is properly configured

### Logs

- **Backend logs**: Check the terminal where you ran `npm run dev`
- **Frontend logs**: Check the browser console and terminal where you ran `npm run dev`

## Technologies Used

### Frontend
- **Next.js 15** - React framework
- **TypeScript** - Type safety
- **Tailwind CSS** - Styling
- **React Hooks** - State management

### Backend
- **Node.js** - Runtime environment
- **Express.js** - Web framework
- **TypeScript** - Type safety
- **PostgreSQL** - Database
- **pg** - PostgreSQL client for Node.js
- **CORS** - Cross-origin resource sharing

## Development

### Running in Development Mode

1. **Start the database** (if not already running)
2. **Start the backend**:
   ```bash
   cd backend
   npm run dev
   ```
3. **Start the frontend** (in a new terminal):
   ```bash
   cd frontend
   npm run dev
   ```

### Building for Production

1. **Build the backend**:
   ```bash
   cd backend
   npm run build
   ```

2. **Build the frontend**:
   ```bash
   cd frontend
   npm run build
   ```

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

## 🚀 Deployment Options

### **Option 1: Supabase (Recommended)**
Since you already have a Supabase project, this is the easiest option:

1. **Get your Supabase connection details:**
   - Go to your Supabase project dashboard
   - Navigate to Settings > Database
   - Copy the connection details

2. **Update backend/.env:**
   ```env
   DB_HOST=your-supabase-host.supabase.co
   DB_PORT=5432
   DB_NAME=postgres
   DB_USER=postgres
   DB_PASSWORD=your-supabase-password
   PORT=5000
   ```

3. **Create the users table in Supabase:**
   ```sql
   CREATE TABLE IF NOT EXISTS users (
       id SERIAL PRIMARY KEY,
       username VARCHAR(255) NOT NULL,
       email VARCHAR(255) UNIQUE NOT NULL,
       is_active BOOLEAN DEFAULT true,
       created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
   );
   ```

### **Option 2: ElephantSQL (Free)**
- Sign up at [elephantsql.com](https://www.elephantsql.com)
- Create a "Tiny Turtle" (free) instance
- Use the provided connection details

### **Option 3: Railway (Free)**
- Sign up at [railway.app](https://railway.app)
- Create a PostgreSQL database
- Use the provided connection details

## 📦 Production Deployment

### **Frontend (Vercel/Netlify)**
1. Connect your GitHub repository
2. Set build command: `npm run build`
3. Set output directory: `.next`
4. Deploy!

### **Backend (Railway/Heroku)**
1. Connect your GitHub repository
2. Set environment variables
3. Deploy!

## License

This project is licensed under the ISC License.
