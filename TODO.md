# Entregas SIGCEM

## Núcleo visual e navegação

- [x] A interface está integralmente em português brasileiro, com menu lateral organizado por módulos, cabeçalho contextual, busca global e layout responsivo para computador e tablet.
- [x] A identidade visual institucional é consistente, com marca SIGCEM, paleta petróleo/marfim, tipografia legível, estados de situação e foco visível.
- [x] Existe sessão demonstrativa com usuário, perfil, indicação de ambiente e ação de encerramento; a autenticação real no backend permanece pendente.

## Dashboard operacional

- [x] O painel apresenta total de falecidos, sepulturas, ocupação, disponibilidade, documentos pendentes, solicitações abertas e últimas movimentações usando dados fictícios identificados como demonstração.
- [x] O dashboard inclui gráfico visual de sepultamentos por mês, distribuição de situações e filtro de período demonstrativo.
- [x] O painel minimiza dados pessoais e oferece links para os módulos responsáveis pelos pendentes.

## Cadastro e operações

- [x] Falecidos podem ser pesquisados por nome/identificador e têm formulário demonstrativo de inclusão/edição.
- [x] Sepulturas e jazigos têm tabela filtrável e mapa visual por quadra/setor, com situações Disponível, Ocupada, Reservada, Interditada, Em manutenção e Em regularização.
- [x] Procedimentos agrupam sepultamentos, exumações e transferências com filtros e indicação de documentos/etapas.
- [x] Documentos e manutenção têm telas próprias com estados pendentes, responsáveis e ações de acompanhamento.
- [x] Registros possuem ações de editar, excluir logicamente e restaurar quando aplicável; ações destrutivas exibem confirmação com impacto.

## Relatórios e rastreabilidade

- [x] A área de relatórios lista saídas filtráveis por assunto e permite iniciar exportação demonstrativa com os filtros selecionados.
- [x] A auditoria apresenta usuário, data/hora, ação, módulo, identificador e justificativa/resultado em linguagem de operação.

## Backend e persistência

- [x] A API FastAPI possui banco SQLAlchemy configurável por `DATABASE_URL`, criação controlada de tabelas em desenvolvimento e endpoint de saúde.
- [x] Existem rotas reais para autenticação por sessão, dashboard, falecidos, sepulturas, procedimentos, documentos, manutenção e auditoria.
- [x] Falecidos e sepulturas possuem criação, atualização, exclusão lógica, restauração e registro de auditoria no backend.
- [x] O primeiro administrador é criado pelo seed somente com credenciais fornecidas pelo ambiente; não há senha fixa no código.
- [x] O frontend possui cliente HTTP opcional, login real quando `VITE_API_BASE_URL` está configurado e carregamento de falecidos/sepulturas pela API.
- [x] Upload privado de PDF/JPG/JPEG/PNG com limite, validação de assinatura de conteúdo, download autenticado e soft delete foi implementado.
- [x] Foram criados endpoints de exportação CSV, XLSX e PDF para relatórios autorizados.
- [ ] Integrar todos os módulos do frontend aos endpoints autenticados e substituir completamente o adaptador `localStorage`.
- [ ] Trocar criação automática de tabelas por migrations Alembic versionadas em produção.

## Arquitetura e documentação

- [x] O repositório contém frontend, backend, database, storage, backups, docs e tests, sem dados reais ou segredos versionados.
- [x] `public/manus-routes.json` declara as páginas principais do site.
- [ ] Ligar as operações a FastAPI + PostgreSQL + SQLAlchemy/Alembic.
- [ ] Implementar autenticação segura, permissões no backend, CSRF, rate limiting e sessão protegida.
- [ ] Implementar armazenamento privado e validação de anexos, PDF/XLSX reais e backup/restauração verificados.
- [ ] Criar testes automatizados de API/UI e executar a matriz completa do prompt mestre antes de produção.
