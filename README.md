# Pipeline de agentes para Next.js e TanStack

Modelo de uma pipeline de agentes de IA para o Claude Code e o Codex, pensada para as bibliotecas de `ia/regras/bibliotecas.md`. Ainda não há aplicação aqui: no início do projeto, este README dá lugar ao da aplicação.

## O que vem no modelo

- `AGENTS.md`: o que todo agente lê primeiro.
- `ia/`: o fluxo, os contratos dos subagentes, as regras por assunto e os fatos do projeto. Uso e estrutura em `ia/README.md`.
- `.claude/` e `.codex/`: os agentes `executor-1` a `executor-5` e `auditor`, e a configuração de cada ferramenta.

## Como começar

1. Copie o repositório para o destino, ou use-o como template.
2. Abra uma sessão do Claude Code ou do Codex na raiz.
3. Peça o que quer construir. Enquanto `ia/fatos.md` disser `modelo`, a sessão principal segue `ia/quando/inicio.md`.

## Conferir o formato

```sh
npx prettier@3.6.2 --check .
```
