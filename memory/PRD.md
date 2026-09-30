# Projeto SEDUC-PA / Concurso — PRD

## Origem
Clone do repo GitHub `isildsouti-cyber/projector-seduc-pa-001` na sandbox Emergent (/app).
Stack: FastAPI (backend) + React CRA (frontend, servido via `yarn start`/craco) + MongoDB.

## Arquitetura
- Backend: /app/backend (server.py, admin_routes.py, pix_generator.py)
- Frontend: /app/frontend — páginas reais são HTML estáticos em `public/` (inicio.html, inscricao.html, etc.)
  e painel admin React build em `public/donaspainel/`.
- Admin: rota /donaspainel (login), documentos em /donaspainel-documentos.html
- Admin user: donas / Seinao10@@ (seed_admin no startup, fallback ADMIN_USERNAME/ADMIN_PASSWORD)
- JWT_SECRET forte configurado em backend/.env

## Implementado (histórico)
- 2026-09-30: Clone + configuração inicial. Deps instaladas, JWT_SECRET forte, build, serviços OK.
  Validado: GET /api/ (200), login admin (JWT), rota protegida /api/admin/auth/me (200 c/ token, 401 sem).
- 2026-09-30: Modal informativo da home (inicio.html) — texto atualizado p/ "quinta-feira, 01/10/2026".
- 2026-09-30: Upload de documentos na inscrição agora aceita QUALQUER formato (foto, print, PDF, etc.).
  - inscricao.html: removido `accept` restritivo; fileToB64 preserva data URL completo (mime real).
  - admin_routes.py: /admin/documentos retorna frente_mime/verso_mime; serve arquivo com content-type
    correto (data URL) + Content-Disposition; ZIP usa extensão certa por mime (_ext_for_mime).
  - donaspainel-documentos.html: imagem = miniatura (modal zoom); PDF/outros = link "Ver PDF"/"Ver arquivo".
  - Verificado por curl: image/png e application/pdf preservados; ZIP gera frente.png/verso.pdf.

## Backlog / Próximos
- P2: Preview inline de PDF dentro do modal do painel (hoje abre em nova aba).
- P2: Mostrar o tipo/extensão do arquivo como badge na listagem.
