# Plano de implementação — SIGCEM

## Escopo desta entrega

Construir um console web responsivo, em português brasileiro, para a gestão diária de um cemitério municipal. A primeira etapa entrega o núcleo operacional navegável com dashboard, pesquisa global, cadastros de falecidos, sepulturas, procedimentos, documentos, manutenção, relatórios, auditoria, sessão de usuário, filtros, edição, exclusão lógica e restauração. Os dados desta etapa são fictícios e persistidos no navegador para permitir validação da experiência sem versionar dados reais.

A arquitetura manterá separação para evolução segura: `frontend/` para React + TypeScript, `backend/` para FastAPI, `database/` para migrações e seeds, `storage/` para arquivos privados, `backups/` para artefatos fora do Git, `docs/` para operação e `tests/` para automação. A próxima etapa pode ligar as mesmas operações a PostgreSQL, SQLAlchemy, Alembic e autenticação de sessão no backend.

## Abordagem de implementação

- React + TypeScript + Vite para a interface.
- CSS próprio com tokens de design para uma interface institucional consistente, sem depender de imagens decorativas genéricas.
- Estado local com `localStorage` apenas para demonstração controlada; os dados são identificados como demonstrativos na interface.
- Componentes orientados a módulos, com uma casca de aplicação compartilhada, tabelas reusáveis, drawer/modal de formulário, toast e confirmação destrutiva.
- Dados iniciais fictícios cobrindo situações variadas para que o dashboard, mapa e relatórios tenham conteúdo útil.
- Rota-manifest estático em `public/manus-routes.json`, incluindo as páginas principais.
- Backend e documentação preparados como contratos iniciais, sem fingir que o banco de produção já está conectado.
- Cliente HTTP opcional por `VITE_API_BASE_URL`: quando configurado, falecidos e sepulturas são carregados da API; sem a variável, o Preview usa o conjunto fictício local.

## Estrutura do projeto

- `src/`: aplicação React, domínio de dados demonstrativos, componentes de layout e estilos.
- `public/`: manifesto de rotas e favicon.
- `backend/app/`: esqueleto FastAPI organizado por rotas, modelos, schemas, serviços e segurança.
- `database/migrations/` e `database/seeds/`: pontos de entrada para PostgreSQL/Alembic.
- `storage/` e `backups/`: diretórios locais ignorados para arquivos e cópias.
- `docs/`: instalação, manual, banco e backup.
- `tests/`: contratos e espaço para testes de API e UI.

## Direção de design

### Estilos considerados

1. **Civic Data Editorial** — 0,07. Interface municipal contemporânea com tipografia editorial, cartões suaves e acentos de sinalização.
2. **Quiet Archive** — 0,05. Arquivo digital sóbrio, com tons de papel, linhas finas e foco em leitura.
3. **Civic Command Center** — 0,08. Painel operacional de alto contraste, com azul petróleo e marcadores de status.

Escolhido: **Civic Data Editorial**.

### Design Movement

Uma fusão entre design de serviços públicos digitais e editorial de dados: estrutura operacional densa, mas com ritmo de leitura, hierarquia forte e sinais de status imediatamente compreensíveis.

### Core Principles

- **Clareza antes da decoração:** cada ação e situação deve ser entendida sem treinamento técnico.
- **Dignidade documental:** os dados são apresentados com sobriedade, sem excesso de exposição pessoal.
- **Orientação por evidência:** indicadores, origem dos dados e trilha de auditoria ficam próximos das ações.
- **Segurança visível:** estados, permissões e operações destrutivas têm linguagem explícita.

### Color Philosophy

Azul petróleo comunica confiança institucional e estabilidade; marfim quente reduz o aspecto frio de sistemas administrativos; verde sálvia sinaliza disponibilidade e conclusão sem parecer financeiro; âmbar e coral aparecem somente em alertas e estados que exigem atenção. O resultado é um produto municipal humano, não militarizado.

### Layout Paradigm

Uma navegação lateral fixa funciona como “corredor administrativo”, enquanto a área principal se comporta como uma folha de trabalho com cabeçalho contextual, faixa de indicadores e painéis assimétricos. O mapa e as tabelas ocupam a largura conforme a tarefa, evitando uma grade rígida de cards idênticos.

### Signature Elements

- Marca SIGCEM em forma de monograma geométrico, combinando uma lápide abstrata com um ponto de localização.
- Chips de situação com ponto de cor e texto, sempre acompanhados de valor ou contexto.
- Linha vertical de atividade recente, como um livro de protocolo contemporâneo.

### Interaction Philosophy

A interface deve responder imediatamente: filtros atualizam a leitura, ações confirmam o resultado com mensagens curtas e operações destrutivas mostram impacto antes da confirmação. Formulários usam campos familiares, ajuda contextual e preservam o foco do servidor no fluxo administrativo.

### Animation

Movimentos curtos de 160–220ms: fade-up discreto para painéis, transição de largura no sidebar, escala mínima em botões e entrada lateral para drawers. Nenhum movimento deve competir com números ou alertas. Respeitar `prefers-reduced-motion`.

### Typography System

`Manrope` para títulos, números e navegação; `Inter` para textos, tabelas e formulários. Títulos usam peso 700–800, corpo 400–500, metadados 12–13px com espaçamento controlado. Números de indicadores usam alinhamento tabular para leitura comparativa.

### Brand Essence

O SIGCEM organiza registros, espaços e procedimentos municipais para que cada decisão cotidiana seja rastreável, segura e humana. Personalidade: **confiável, serena, precisa**.

### Brand Voice

Headlines são objetivas e orientadas à situação; CTAs usam verbos claros; microcopy explica a consequência, sem juridiquês desnecessário.

Exemplos:
- “A operação do cemitério, em uma visão responsável.”
- “Revise os pendentes antes de fechar o expediente.”

### Wordmark & Logo

Monograma “S” modular dentro de um pino de localização retangular, acompanhado do wordmark SIGCEM em caixa alta e subtítulo “Gestão de cemitérios”. Na interface, a versão reduzida é um pino formado por dois blocos que sugerem quadra e registro.

### Signature Brand Color

**Petróleo SIGCEM — `#174A52`**, usado em navegação e ações primárias.

## Dependências e limites

Nenhum dado real deve ser inserido. A camada local é explicitamente demonstrativa e deve ser substituída por API autenticada antes de produção. Recursos críticos como backup real, restauração, PDF/XLSX, anexos privados e controle de acesso no backend permanecem como próximos contratos de implementação, documentados sem botões falsos na interface.
