# Projeto

> Para: orquestrador e revisor · Leia quando: o orquestrador, em toda tarefa; o revisor, as seções `Checagens` e `Rodar`.

Fatos conferidos deste projeto que o código não mostra. Critérios: `guias/escrita.md › Projeto`.

## Adoção

- Estado: template, sem aplicação.

## Idioma

- Mensagens de commit: Conventional Commits, com a descrição em português do Brasil.
- Código e documentação: COD-12. Interface: UI-11.

## Checagens

### Completas

- Pipeline: a conferência de `guias/escrita.md › Conferência`, quando a tarefa muda `pipeline/`, `AGENTS.md`, `.claude/` ou `.codex/`.
- Formato: `npx prettier@3.6.2 --check .`.
- Diff: `git status --short --untracked-files=all` e `git diff --check`, incluindo os arquivos novos na leitura.

### Com escopo

- Formato: `npx prettier@3.6.2 --check <arquivos>`.

### Pré-requisitos

- Node.js, para o Prettier. O `npx` baixa o Prettier do npm na primeira execução.

### Marcadores de supressão

- Nenhum: o template não tem ferramenta de código instalada.

## Rodar

- Nada a rodar: o template não tem aplicação.

## Paralelismo

- Limite: até 10 missões ao mesmo tempo, reduzido à capacidade da ferramenta ou da conta.
- Recursos exclusivos: nenhum registrado.
- Agregadores: nenhum registrado.

## Arquivos protegidos

Cada item tem a regra `ask` correspondente em `.claude/settings.json`: `Edit(/<arquivo>)` para arquivo e `Edit(/<pasta>/**)` para pasta.

- Instruções e ferramentas de agente: `AGENTS.md`, `CLAUDE.md`, `.claude/` e `.codex/`.
- Processo da pipeline: `pipeline/README.md`, `pipeline/guias/`, `pipeline/papeis/` e `pipeline/projeto.md`.
- Conhecimento que governa a leitura e as dependências: `pipeline/conhecimento/indice.md` e `pipeline/conhecimento/stack.md`.
- Repositório: `.gitattributes`.

Configuração protegida é a que define checagens, framework, tipos, dependências e comandos, infraestrutura e dados, hooks e integração contínua. Ao criá-la ou adotá-la, registre aqui o caminho real e, na mesma entrega, a regra `ask` correspondente, antes de delegar mudanças nela.

## Ambiente

- Ferramentas de agente: Claude Code, com as definições em `.claude/agents/`, e Codex, com as de `.codex/agents/`. As duas pastas têm os mesmos agentes.
- Disponibilidade dos modelos na conta do humano: não conferida no template. Indisponibilidade real é declarada, sem troca silenciosa de agente.
