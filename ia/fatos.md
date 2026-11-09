# Fatos do projeto

Só o que foi conferido e o código não mostra.

## Estado

`modelo`: a pipeline sem aplicação. Passa a `em uso` por `ia/quando/inicio.md`.

## Checagens

### Completas

- Formato: `npx prettier@3.6.2 --check .`
- Diff: `git status --short --untracked-files=all` e `git diff --check`, lendo também os arquivos novos.

### Com escopo

- Formato: `npx prettier@3.6.2 --check <arquivos>`

### Pré-requisitos

- Node.js. O `npx` baixa o Prettier na primeira execução.

### Supressões

- Nenhum marcador: não há ferramenta de código instalada.

## Rodar

Nada a rodar: não há aplicação.

## Paralelo

- Limite: 10 encomendas ao mesmo tempo, ou menos, se a ferramenta ou a conta não comportar.
- Recursos exclusivos: nenhum.
- Agregadores: nenhum.

## Agentes

- Claude Code: `.claude/agents/`. Codex: `.codex/agents/`. O modelo e o esforço de cada nível estão nessas definições.
- Disponibilidade dos modelos na conta do humano: não conferida. Modelo indisponível é declarado; nunca troque de agente em silêncio.
- No Claude Code, o `tools` de cada definição é lista fechada. Ferramenta que falta a um executor é proposta (`ia/quando/reparo.md › Só com o humano`).

## Idioma

- Commits: Conventional Commits, com a descrição em português do Brasil.
- Código e documentação: `ia/regras/codigo.md › C8`. Interface: `ia/regras/visual.md › V11`.
