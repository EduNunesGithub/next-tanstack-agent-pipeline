# Projeto

> Como este projeto se conecta à pipeline. Arquivo protegido: só muda com aprovação do humano.
> Aponte para os arquivos onde a verdade está; não copie o conteúdo deles.

## Estado do projeto

- Aplicação Next.js com App Router em `src/app/`, instalada manualmente com npm. Dependências e versões: `package.json` e `package-lock.json`.
- Não há legado nem padrões concorrentes.
- Origem da pipeline: Pipeline v4, derivada da [Pipeline v3](https://github.com/EduNunesGithub/ai-first-pipeline), commit `f80d84485f42fb647ed4c8172daaa7e3031eccbc`, cujos arquivos genéricos vieram de `modelo/`.
- Git: branch principal `master`.

## Convenções

- Documentação e descrição dos commits: português do Brasil, em Conventional Commits (`feat: ...`, `fix: ...`).
- Identificadores no código: inglês.
- Nomes de arquivos e pastas do produto: kebab-case, respeitando os nomes exigidos pelas ferramentas.
- Textos da interface: português do Brasil.

## Fontes de referência

- Stack e ferramentas: documentação oficial vinculada no `README.md`.
- Dependências, requisitos de execução e comandos: `package.json`; resolução reproduzível: `package-lock.json`.
- Tipos e aliases da aplicação: `tsconfig.json`; aliases nativos do Node.js: `imports` em `package.json`; lint e ordenação: `eslint.config.mjs` e `eslint/`; configuração do Next.js: `next.config.mts`; formato: `.prettierrc.json` e `.prettierignore`.
- Tailwind CSS: `postcss.config.mjs` e `src/app/globals.css`; usar o tema padrão do Tailwind enquanto não houver tema próprio.
- Testes: configuração unitária em `vitest.config.mts`; configuração e2e em `playwright.config.ts`; comandos, instalação do navegador e fontes oficiais em `README.md`.
- Tipografia global e preparação dos portais Base UI: `src/app/globals.css` e `src/app/layout.tsx`; composição e animação: documentação oficial vinculada no `README.md`.
- Hooks Git: `.husky/pre-commit` e `.husky/commit-msg`, instalados pelo script `prepare`; convenção das mensagens: `commitlint.config.mjs`.

## Checagens

**Completa**: as checagens do orquestrador. **Ficha**: o comando com escopo que entra em `Feito quando`; `—` quando não há.

| Checagem | Completa | Ficha |
| --- | --- | --- |
| Build | `npm run build`. | — |
| Commit | `npm run commitlint -- --from HEAD~1 --to HEAD --verbose`; o hook `commit-msg` verifica a mensagem de cada novo commit. | — |
| Diff e whitespace | `git status --short --untracked-files=all` e `git diff --check`; incluir os arquivos novos na leitura. Antes de serem rastreados, verificar whitespace com `git diff --no-index --check -- NUL <arquivo>` no Windows. | — |
| Formato | `npm run format:check`. | `npx prettier --check <arquivos>` |
| Lint | `npm run lint`. | `npx eslint <arquivos>` |
| Testes unitários | `npm test`. Vitest com Testing Library em jsdom. | `npx vitest run <pasta>` |
| Testes e2e | Quando houver suíte e2e, `npm run test:e2e`; o comando inclui o build e gerencia o servidor de produção. Atualmente não há suíte e2e. | — |
| Tipos | `npm run typecheck`, incluindo a geração dos tipos Next.js antes de `tsc`. | — |

Na conferência de arquivo novo com `--no-index --check`, o status 1 pode indicar apenas que o arquivo difere de `NUL`; erros de whitespace são listados na saída e precisam ser corrigidos.

Marcadores de supressão: `eslint-disable`, `eslint-enable`, `eslint-env`, `prettier-ignore`, `@ts-ignore`, `@ts-expect-error`, `@ts-nocheck`, `ignoreBuildErrors`. Diretivas geradas em `next-env.d.ts` são referências de tipos, não supressões.

## Paralelismo

- Limite por onda: 10 fichas.
- Arquivos compartilhados: `src/app/globals.css`, `src/app/layout.tsx` e qualquer arquivo que agregue vários módulos (índices de reexportação, registros, rotas).
- Recursos exclusivos: as checagens da coluna Completa, `npm run dev` e `npm start` (porta 3000) e a pasta `.next/`.

## Rodar e observar o produto

- Instalar de forma reproduzível: `npm ci`. O script `prepare` ativa o Husky no repositório Git.
- Desenvolvimento: `npm run dev`; endereço padrão `http://localhost:3000`.
- Produção local: `npm run build` e `npm start`; mesmo endereço padrão.
- Observar: abrir a página inicial no navegador; conferir a resposta HTTP e a página de rota inexistente.
- Dados e acessos de teste: inexistentes; a página inicial não exige credenciais.
- Limites conhecidos: o terminal em sandbox falhou ao inicializar nesta instalação; o terminal com aprovação automática funcionou. O navegador para controle interativo não estava conectado; Chromium do Playwright está disponível para verificações que precisarem de navegador. Alertas das dependências: `README.md`.

## Arquivos protegidos

Só mudam quando a tarefa exige, e toda mudança é declarada na entrega.

- `AGENTS.md`, `CLAUDE.md`, `.claude/`, `.codex/`.
- `pipeline/`, exceto `pipeline/padroes.md`.
- Configuração das checagens e dos arquivos verificados: `.gitattributes`, `.gitignore`, `.prettierignore`, `.prettierrc.json`, `commitlint.config.mjs`, `eslint.config.mjs`, `eslint/`, `next.config.mts`, `postcss.config.mjs`, `tsconfig.json`, `vitest.config.mts`, `playwright.config.ts`.
- Comandos, dependências e hooks: `.husky/commit-msg`, `.husky/pre-commit`, `package-lock.json`, `package.json`.
- Integração contínua: ainda inexistente; registrar quando criada.

Os caminhos existentes estão nas regras `ask` de `.claude/settings.json`.

## Ferramentas de agente

- `.claude/agents/` e `.codex/agents/`: níveis `t0` a `t3` e `revisor`; modelo e esforço em cada definição. O Codex não oferece Haiku nem Opus e usa equivalentes OpenAI.
- `.claude/settings.json` e `.codex/config.toml`: memória automática desativada, confirmação para comandos git que escrevem e limite de agentes simultâneos do Codex.
- A confiança deste projeto foi conferida na configuração local do Codex: `trust_level = "trusted"`. As configurações locais de projeto só são carregadas em projetos confiáveis, conforme a [documentação oficial](https://learn.chatgpt.com/docs/config-file/config-reference).
- Codex CLI e Claude Code estão instalados. A disponibilidade dos modelos na conta do humano não foi testada com chamadas aos provedores; qualquer indisponibilidade real deve ser declarada, sem substituição silenciosa.
- `next dev`, `next build` e `next typegen` mantêm `next-env.d.ts` e tipos em `.next/`; esses artefatos não são editados manualmente nem versionados.
- `agentRules: false` em `next.config.mts` impede a escrita automática do Next.js nos arquivos de instruções dos agentes.
