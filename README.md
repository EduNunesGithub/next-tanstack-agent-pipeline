# Pipeline de agentes para Next.js e TanStack

Template de uma pipeline de agentes de IA para o Claude Code e o Codex, pensada para a stack de `pipeline/conhecimento/stack.md`. Ainda não há aplicação aqui: na adoção, este README dá lugar ao da aplicação.

## O que vem no template

- `AGENTS.md`: o que todo agente lê primeiro: papéis, leis, conflitos, glossário e o mapa da pipeline.
- `pipeline/`: papéis, guias, conhecimento por área, fatos do projeto e backlog. Uso e estrutura em `pipeline/README.md`.
- `.claude/` e `.codex/`: as definições dos agentes `t0` a `t4` e `revisor`, e as configurações de cada ferramenta.
- `CHANGELOG.md`: a evolução do template, versão a versão.

## Como começar

1. Copie o repositório para o destino ou use-o como template.
2. Abra uma sessão do Claude Code ou do Codex na raiz.
3. Peça o que quer construir. Enquanto `pipeline/projeto.md` indicar o estado de template, a sessão principal segue `pipeline/guias/adocao.md`.

## Conferir o formato

```sh
npx prettier@3.6.2 --check .
```
