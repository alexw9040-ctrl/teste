# SIGCEM — Sistema Integrado de Gestão de Cemitérios

![CI](../../actions/workflows/ci.yml/badge.svg)

O SIGCEM é uma base de console administrativo em português brasileiro para organizar falecidos, sepulturas, procedimentos, documentos, manutenção, relatórios e auditoria de um cemitério municipal.

## Estado atual

O projeto contém uma API FastAPI real com SQLAlchemy, banco configurável por `DATABASE_URL`, autenticação por sessão, perfis, auditoria, soft delete e endpoints para dashboard, falecidos, sepulturas, procedimentos, documentos, manutenção e auditoria. A interface mantém dados demonstrativos locais no Preview para continuar navegável; a integração frontend/API ainda é a próxima etapa do trabalho.

A arquitetura separa React/TypeScript no frontend, FastAPI no backend, PostgreSQL/SQLite, SQLAlchemy, Alembic, storage privado, Docker Compose e testes automatizados. Consulte `plan.md`, `TODO.md` e a pasta `docs/`.

## Executar a API

```bash
python3 -m venv .venv
.venv/bin/pip install -r backend/requirements.txt
export SIGCEM_ADMIN_EMAIL=admin@example.gov.br
export SIGCEM_ADMIN_NAME="Administrador SIGCEM"
export SIGCEM_ADMIN_PASSWORD="defina-uma-senha-forte"
.venv/bin/python backend/scripts/seed_demo.py
.venv/bin/uvicorn backend.app.main:app --reload --port 8000
```

O seed não contém uma senha fixa: as três variáveis administrativas precisam ser fornecidas pelo ambiente ou por um secret manager.

## Comandos

```bash
pnpm install
pnpm dev
pnpm build
pnpm check
```

## Regras de segurança

Não versione dados reais de falecidos, documentos pessoais, backups, bancos de produção, tokens, senhas ou `.env`. Use `.env.example` como referência. A etapa de produção precisa implementar autenticação segura, autorização no backend, proteção CSRF, rate limiting, validação de arquivos, HTTPS, auditoria append-only, backup criptografado e política de retenção conforme LGPD.

## Testes

```bash
pip install -r backend/requirements.txt
python -m pytest -q      # API (SQLite temporário, nada é gravado no seu banco)
pnpm check && pnpm build # frontend
```

O workflow `.github/workflows/ci.yml` roda esses mesmos comandos a cada push e pull request.

## Docker

```bash
cp .env.example .env     # preencha APP_SECRET_KEY e POSTGRES_PASSWORD
docker compose up --build
```

A API sobe em `http://localhost:8000` (documentação em `/api/docs`). Em produção, sirva por HTTPS e use `COOKIE_SECURE=true`; com `APP_ENV=production` a API se recusa a iniciar sem um `APP_SECRET_KEY` forte.

## Publicar no GitHub

```bash
git init -b main
git add .
git status               # confirme que não há .env, *.db, storage/ ou backups/
git commit -m "Primeira versão do SIGCEM"
git remote add origin https://github.com/SEU-USUARIO/SIGCEM.git
git push -u origin main
```

Crie antes o repositório vazio no GitHub (sem README, .gitignore ou licença, para não gerar conflito no primeiro push).
