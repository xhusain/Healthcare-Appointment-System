# Healthcare Appointment System

A full-stack healthcare management application for patient registration, doctor
profiles, appointment workflows, treatment tracking, and notifications.

This repository contains a Next.js client and an Express/MongoDB API. It is
intended as an educational/demo project and is not a production medical
records system.

## Features

- Role-based authentication for administrators, doctors, and patients
- Patient and doctor profile management
- Doctor approval and patient assignment by administrators
- Appointment requests, confirmation, rejection, assignment, and completion
- Treatment records with diagnoses, physical checkups, prescriptions, and
  follow-up visits
- In-app notifications and email notifications
- Dashboard views tailored to each user role

## Technology

- **Frontend:** Next.js, React, TypeScript
- **Backend:** Node.js, Express.js
- **Database:** MongoDB with Mongoose
- **Authentication:** JWT
- **Email:** Nodemailer (SMTP or a temporary Ethereal demo mailbox)

## Project structure

```text
.
├── client/                 # Next.js frontend
│   ├── app/                # Pages and dashboard routes
│   ├── components/         # Reusable UI components
│   ├── context/            # Authentication and toast state
│   └── lib/                # API types and request helper
├── server/                 # Express backend
│   ├── src/
│   │   ├── config/         # Database configuration
│   │   ├── middleware/     # Authentication and shared middleware
│   │   ├── models/         # Mongoose models
│   │   ├── routes/         # REST API routes
│   │   └── utils/          # Email, token, notification, and validation helpers
│   └── scripts/            # Optional demo data and database maintenance scripts
└── package.json            # Root scripts for running both applications
```

## Prerequisites

- Node.js 20 or newer
- npm
- MongoDB running locally, or a MongoDB connection string

## Installation

Clone the repository and install dependencies in the root, client, and server
directories:

```bash
git clone <your-repository-url>
cd healthcare-appointment-system
npm install
cd client && npm install
cd ../server && npm install
cd ..
```

Create local environment files from the committed examples:

```powershell
Copy-Item server\.env.example server\.env
Copy-Item client\.env.example client\.env
```

Edit `server/.env` before starting the application:

- Set `MONGODB_URI` to your local or hosted MongoDB database.
- Replace `JWT_SECRET` with a long, random value.
- Set `SEED_PASSWORD` and `ADMIN_PASSWORD` only if you plan to run the
  optional seed scripts.
- Configure the SMTP variables if real email delivery is required.

The `.env` files are intentionally ignored by Git. Never commit them.

## Running locally

From the repository root, start both applications:

```bash
npm run dev
```

Alternatively, start them separately:

```bash
npm run dev:server
npm run dev:client
```

The client runs at <http://localhost:3000> and the API runs at
<http://localhost:5000>. Check the API with
<http://localhost:5000/api/health>.

## Demo data

After configuring `server/.env`, optional scripts can create demo users and
repair/approve seeded records:

```bash
npm --prefix server run seed:management
npm --prefix server run db:normalize-users
npm --prefix server run db:approve-seeded-doctors
```

The seed scripts use the passwords configured through `SEED_PASSWORD` and
`ADMIN_PASSWORD`; no demo passwords are stored in the repository. Run these
scripts only against a development database because they delete and recreate
selected demo records.

## Useful commands

| Command | Description |
| --- | --- |
| `npm run dev` | Start client and server together |
| `npm run dev:client` | Start only the Next.js client |
| `npm run dev:server` | Start only the API server |
| `npm --prefix client run build` | Create a production client build |
| `npm --prefix client run lint` | Run the client linter |
| `npm --prefix server start` | Start the API without nodemon |

## API overview

The API is namespaced under `/api`:

- `/api/auth` - registration, login, current user, and logout
- `/api/dashboard` - role-specific dashboard data
- `/api/doctors` - doctor profiles and administration
- `/api/patients` - patient profiles and administration
- `/api/appointments` - appointment lifecycle
- `/api/treatments` - treatment records and follow-ups
- `/api/notifications` - notification records
- `/api/health` - service and database status

## Security and privacy

- Environment files, local database settings, secrets, logs, build output, and
  dependency folders are excluded through `.gitignore`.
- Demo credentials are not documented in the repository because they are tied
  to a particular database. Create your own credentials using the registration
  flow or the seed-script environment variables.
- This application is for learning and demonstration only. Do not use it with
  real patient data without a thorough security, privacy, and compliance review.