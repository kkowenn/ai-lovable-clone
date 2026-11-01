# Lovable AI

An AI-powered app builder. Describe what you want, and an autonomous Python agent generates code, runs it in an isolated sandbox, and returns a live preview.

## demo 

[Watch the demo](https://kritsadakruapat.vercel.app/)

## Architecture

```
Next.js app ──► Inngest (background jobs) ──► FastAPI service ──► LangChain agent
     │                                                                  │
     └──────────────► Neon PostgreSQL (Prisma)          E2B sandbox ◄───┘
```

| Component | Role |
|-----------|------|
| **Next.js 15** (App Router, tRPC) | Web UI and API |
| **Inngest** | Event-driven orchestration and background jobs |
| **FastAPI + LangChain** | Python service that runs the autonomous agent |
| **E2B** | Secure sandboxed code execution |
| **Prisma + Neon** | Database access and managed PostgreSQL |
| **Tailwind CSS + shadcn/ui** | Styling and components |

## Quick Start

**Prerequisites:** Node.js 20+, Python 3.11+, Docker, and accounts for Neon, OpenAI and E2B.

**1. Configure environment variables.** Create `.env` (local) or `.env.docker` (Docker):

```env
DATABASE_URL="postgresql://<user>:<password>@<neon-host>/<db>?sslmode=require"
OPENAI_API_KEY="<your-openai-key>"
E2B_API_KEY="<your-e2b-key>"
NEXT_PUBLIC_APP_URL="http://localhost:3000"
```

**2. Run the project.**

```bash
# Option A: local development
chmod +x dev.sh && ./dev.sh

# Option B: Docker
docker compose --env-file .env.docker up --build
```

| Service | URL |
|---------|-----|
| Web app | http://localhost:3000 |
| Inngest dashboard | http://localhost:8288/runs |
| Agent API docs | http://localhost:8000/docs |

**3. Verify the agent service.**

```bash
curl -X POST http://localhost:8000/run-task \
  -H "Content-Type: application/json" \
  -d '{"task": "Summarize recent transcript files."}'
```

## Project Structure

```
src/                  Next.js app, tRPC and Inngest functions
prisma/               Database schema
Agent-Python/         FastAPI + LangChain agent
sandbox-templates/    E2B sandbox templates
docker-compose.yml    Full-stack development environment
dev.sh                Local bootstrap script
```

## Security

Never commit real API keys or `.env` files. Share only placeholder values like the example above.

## License

Add a license here (for example, MIT).
