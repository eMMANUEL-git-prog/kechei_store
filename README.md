# Store Keeping & Inventory Management System

A comprehensive inventory management system built for institutional/camp stores (non-retail). Tracks stock movements, manages goods received notes (GRN), handles stock issues to departments, and maintains complete audit trails.

## Features

### Core Functionality
- **Item Management**: Create and manage inventory items with categories, units, and reorder levels
- **Supplier Management**: Track supplier information and delivery notes
- **Department Management**: Manage internal departments and their stock requests
- **Stock Receiving (GRN)**: Record goods received from suppliers with full traceability
- **Stock Issuing**: Issue items to departments with approval workflows
- **Stock Adjustments**: Handle damaged, expired, or lost items with mandatory reasons
- **Audit Trail**: Complete movement history for every transaction
- **Reporting**: Dashboard with real-time statistics and analytics

### Security
- JWT-based authentication
- Role-based access control (Admin, Storekeeper, Department Head, Auditor)
- No deletion of transactions (audit compliance)
- Stock validation (prevents negative stock)

## Tech Stack

**Backend:**
- Express.js (Node.js)
- PostgreSQL database
- JWT authentication
- bcrypt for password hashing

**Frontend:**
- Next.js 16 (React)
- Tailwind CSS v4
- shadcn/ui components
- TypeScript

## Project Structure

```
├── backend/
│   ├── config/         # Database configuration
│   ├── database/       # SQL schemas and seed data
│   ├── middleware/     # Auth middleware
│   ├── routes/         # API endpoints
│   ├── server.js       # Express server
│   └── package.json
├── app/
│   ├── dashboard/      # Dashboard pages
│   ├── page.tsx        # Login page
│   └── layout.tsx
└── components/         # React components
```

## Getting Started

### Prerequisites
- Node.js 18+ installed
- PostgreSQL 14+ installed
- Git

### Step 1: Database Setup

```bash
# Create database
createdb store_inventory

# Run migrations
cd backend
psql -d store_inventory -f database/001_init_schema.sql
psql -d store_inventory -f database/002_seed_data.sql
```

See `backend/database/README.md` for detailed database setup instructions.

### Step 2: Backend Setup

```bash
cd backend
npm install

# Copy environment variables
cp .env.example .env

# Edit .env and update:
# - DATABASE_URL (PostgreSQL connection string)
# - JWT_SECRET (secure random string)
# - PORT (default: 5000)

# Start backend server
npm run dev
```

The backend will run at `http://localhost:5000`

### Step 3: Frontend Setup

```bash
# From project root
npm install

# Start Next.js development server
npm run dev
```

The frontend will run at `http://localhost:3000`

### Step 4: Login

Use these default credentials:
- **Admin**: username: `admin`, password: `admin123`
- **Storekeeper**: username: `storekeeper`, password: `admin123`

**⚠️ Change these passwords in production!**

## API Documentation

### Authentication
All endpoints require JWT token in Authorization header:
```
Authorization: Bearer <token>
```

### Key Endpoints
- `POST /api/auth/login` - User login
- `GET /api/items` - Get all items
- `GET /api/stock/levels` - Get stock levels
- `GET /api/stock/low-stock` - Get low stock alerts
- `POST /api/grn` - Create Goods Received Note
- `POST /api/issues` - Create stock issue
- `GET /api/reports/dashboard-stats` - Dashboard statistics

See `backend/README.md` for complete API documentation.

## Database Schema

### Core Tables
- **users**: System users with roles
- **items**: Inventory items
- **categories**: Item categories
- **units_of_measure**: Units (kg, pcs, liters)
- **stock**: Current stock balances
- **suppliers**: Supplier records
- **departments**: Organizational units

### Transaction Tables
- **goods_received_notes**: Incoming stock
- **grn_items**: GRN line items
- **stock_issues**: Outgoing stock
- **stock_issue_items**: Issue line items
- **stock_adjustments**: Manual corrections
- **stock_movements**: Complete audit trail

## User Roles

1. **Admin**: Full system access, user management
2. **Storekeeper**: Create GRNs, issue stock, manage items
3. **Department Head**: Request items, view department history
4. **Auditor**: Read-only access for auditing

## Development

```bash
# Backend (with hot reload)
cd backend
npm run dev

# Frontend
npm run dev
```

## Production Deployment

1. Set `NODE_ENV=production`
2. Use strong `JWT_SECRET`
3. Enable PostgreSQL SSL
4. Change all default passwords
5. Set proper CORS origins
6. Use environment variables for all secrets

## License

MIT

## Support

For issues and questions, please open a GitHub issue.
# kechei_store
