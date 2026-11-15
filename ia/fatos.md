# Fatos do projeto

O que um agente precisa para operar e nem o código nem o `README.md` mostram. Só o que foi conferido. Instalar, rodar e checar: `README.md`.

## Estado

`modelo`: a pipeline sem aplicação. Passa a `em uso` por `ia/quando/inicio.md`.

## Checagens

- Completas: as de `README.md`, mais o diff: `git status --short --untracked-files=all` e `git diff --check`, lendo também os arquivos novos.
- Com escopo:
  - Formato: `npx prettier@3.6.2 --check <arquivos>`

## Paralelo

- Limite: 10 encomendas ao mesmo tempo, ou menos, se a ferramenta ou a conta não comportar.
- Recursos exclusivos: nenhum.
- Agregadores: nenhum.

## Armadilhas

O que rodar ou checar não avisa e já custou tempo. Nenhuma.
