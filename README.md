# PulseWatch

PulseWatch é um monitor de uptime inspirado no Uptime Kuma, com backend em **Node.js + TypeScript + Fastify**, frontend em **SvelteKit**, banco **PostgreSQL**, ORM **Prisma**, WebSocket em tempo real e Docker Compose.

## Funcionalidades

- Login com JWT e senha criptografada
- Usuário admin inicial criado automaticamente
- CRUD de monitores
- Monitores HTTP, TCP, DNS e Ping
- Engine de checagem com intervalo individual por monitor
- Status: `UP`, `DOWN`, `DEGRADED`, `PAUSED`, `UNKNOWN`
- Histórico de checagens com latência, erro e código HTTP
- Dashboard com totais, uptime geral e lista em tempo real
- WebSocket para atualizar o painel quando cada check finaliza
- Incidentes automáticos quando um monitor cai e recuperação quando volta
- Canais de notificação: Webhook, Discord, Telegram e estrutura para e-mail
- Status page pública por slug
- Dockerfile para backend e frontend
- `docker-compose.yml` com PostgreSQL, Redis, backend e frontend

## Rodar com Docker

```bash
cp .env.example .env
docker compose up --build
```

Acesse:

```txt
Frontend: http://localhost:4173
Backend:  http://localhost:3000
Health:   http://localhost:3000/health
```

Usuário padrão:

```txt
E-mail: admin@pulsewatch.local
Senha: admin123
```

Altere esses dados no `.env` antes de publicar em produção.

## Endpoints principais

```txt
POST   /api/auth/login
GET    /api/auth/me
GET    /api/dashboard
GET    /api/monitors
POST   /api/monitors
GET    /api/monitors/:id
PATCH  /api/monitors/:id
DELETE /api/monitors/:id
POST   /api/monitors/:id/pause
POST   /api/monitors/:id/resume
POST   /api/monitors/:id/run-now
GET    /api/monitors/:id/checks
GET    /public/status/:slug
```

## Próximos passos

- Criar migrations versionadas do Prisma
- Adicionar testes automatizados na engine
- Criar retenção automática para histórico antigo
- Evoluir alertas por e-mail real
- Separar engine em worker dedicado quando crescer
