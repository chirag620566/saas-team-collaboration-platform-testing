# Project Management & Team Collaboration SaaS

A web app where teams keep projects, tasks, deadlines and progress in one place. People register their organization, create projects, add tasks to a Kanban board, assign them to teammates and watch progress on a dashboard. Each organization only ever sees its own data.

Built as the team project for the Qveto Technologies Web Development Internship.

## What it does
- Register an organization and log in (passwords are hashed, tokens expire)
- Three roles: **owner**, **manager**, **employee**
- Projects with a key, due date and members
- Tasks with priority, due date, assignee, labels and subtasks
- Kanban board with drag and drop (and a dropdown as the keyboard alternative), search and filters
- Dashboard with task counts, overdue tasks and completion rate
- Separate data for every organization

## Tech stack
| Part | Technology |
|---|---|
| Frontend | React 18, Vite |
| Backend | Node.js, Express |
| Database | MongoDB with Mongoose (an in-memory demo store is used if MongoDB is not running) |
| Auth | JWT, bcrypt |
| Tests | Node's built-in test runner (`node --test`) |

## Folder structure
```
frontend/    React app
backend/     Express API (routes, controllers, models, middlewares, tests, seeds)
docs/        API spec, architecture, user flows, demo guide, test cases
scripts/     run-project.bat (Windows helper)
```

## Getting started
You need Node.js 18 or newer. MongoDB is optional for trying the app out.

```bash
# 1. install everything
npm install
npm run install:all

# 2. create your settings file
cp backend/.env.example backend/.env      # on Windows: copy backend\.env.example backend\.env

# 3. (only if MongoDB is running) load the demo data
npm run seed

# 4. start backend and frontend together
npm run dev
```
Open http://localhost:3000. The API runs on http://localhost:5000 and `http://localhost:5000/api/health` shows which database is in use.

On Windows you can also double-click `scripts/run-project.bat`.

If MongoDB is not running, the backend prints a warning and uses an in-memory database with the same demo data. Everything works, but data is lost when the server stops. Set `ALLOW_MEMORY_DB=false` in `.env` if you would rather it refuse to start.

## Demo accounts
All three belong to "Apex Innovations Corp". Password for all: `Password123!`

| Role | Email |
|---|---|
| Owner | owner@apex.com |
| Manager | manager@apex.com |
| Employee | dev@apex.com |

Registering a new account creates a separate organization, which is also how you can show that two organizations cannot see each other's data.

## Settings (`backend/.env`)
| Name | Meaning |
|---|---|
| `PORT` | API port (default 5000) |
| `MONGO_URI` | MongoDB connection string |
| `JWT_SECRET` | Long random text used to sign tokens. Required when `NODE_ENV=production` |
| `JWT_EXPIRES_IN` | Token lifetime, for example `7d` |
| `CORS_ORIGIN` | Frontend addresses allowed to call the API |
| `ALLOW_MEMORY_DB` | `false` stops the server instead of using the in-memory store |

Never commit the real `.env` file. Only `.env.example` belongs in Git.

## Running the tests
```bash
npm test
```
This runs the 39 API tests in `backend/tests/api.test.js` against the in-memory store (they never touch a real database). More detail is in `docs/test-cases.md`.

## Documentation
- `docs/API_SPECIFICATION.md` : every endpoint
- `docs/system-architecture.md` : how the pieces fit together
- `docs/user-flows.md` and `docs/demo-guide.md` : walkthroughs
- `docs/Requirements_and_User_Flows.md` : requirements
- `docs/Test_Cases_and_Bug_Log.xlsx` : manual test checklist and bug log

## Git workflow
Each member works on their own branch and commits in small steps. The team lead merges into `main`. No `.env`, `node_modules`, `dist` or uploaded files in commits (the `.gitignore` already covers them).

## Team
| Member | Role |
|---|---|
| Member 1 | Team lead, integration |
| Member 2 | Frontend |
| Member 3 | Backend API |
| Member 4 | Database and authentication |
| Member 5 | Testing and documentation |

(Replace with real names before submitting.)

## Known limitations
- The tests and the fixes were checked with the in-memory store. They have not been run against a real MongoDB, so do that once before the review.
- The Qveto project document lists MySQL or PostgreSQL as the database. This project uses MongoDB. Confirm with the mentor that this is accepted.
- There is no screen yet to invite teammates. Registration always creates a new organization with one owner; the demo organization already has a manager and an employee.
- Comments, file attachments and email notifications are not built.
- The login rate limit is kept in server memory, so it resets when the server restarts.
- The React screens have not been click-tested by an automated tool.
