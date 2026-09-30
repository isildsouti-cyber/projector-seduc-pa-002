# PRD — projector-SES-TO-001 (Painel Administrativo Concurso SES/TO)

## Origem
Clone do repo GitHub https://github.com/kim44870288-crypto/projector-SES-TO-001 na sandbox Emergent (/app).
Data setup: 30/09/2026.

## Stack
- Backend: FastAPI (Python) — /app/backend (server.py + admin_routes.py + pix_generator.py)
- Frontend: React CRA (craco) — /app/frontend
- Banco: MongoDB (MONGO_URL/DB_NAME do backend/.env, não alterados)

## Config preservada / adicionada
- backend/.env: MONGO_URL, DB_NAME, CORS_ORIGINS (preservados) + JWT_SECRET forte adicionado
- frontend/.env: REACT_APP_BACKEND_URL (preservado)
- package.json: adicionado `resolutions.electron-to-chromium = 1.5.442` (a 1.5.443 estava com tarball 404 no registry, quebrava o yarn install)

## Rotas chave
- GET /api/ → {"message":"Painel Administrativo API"}
- POST /api/admin/auth/login → {token, user}
- GET /api/admin/auth/me (protegida, Bearer JWT)
- /api/pix/generate, /api/pix/qr.png, /api/pix/code.txt (dependem de pix_generator.py — presente)
- Rota admin frontend: /donaspainel

## Status (30/09/2026)
- Backend + Frontend rodando (supervisor).
- Todas validações do usuário passaram (GET /api/, login, rota protegida com JWT).

## Backlog / Next
- Cadastrar chave PIX pelo painel admin (seed de pix_config está desabilitado no startup).
