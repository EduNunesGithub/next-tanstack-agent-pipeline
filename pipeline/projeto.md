# Projeto

## Estado de adoção

- Estado: template, sem aplicação.

## Convenções

- Idioma: documentação, descrição dos commits e textos da interface em português do Brasil; identificadores no código em inglês.
- Nomes de arquivos e pastas do produto: kebab-case, respeitando os nomes exigidos pelas ferramentas.

## Fontes de referência

- Nenhuma registrada.

## Checagens

- No template: a sintaxe de `.claude/settings.json` e dos arquivos de `.codex/`, o formato do Markdown e as referências entre os arquivos da pipeline.

## Paralelismo

- Limite por onda: até 10 fichas, reduzido à capacidade disponível na ferramenta ou conta. Falta de vagas divide a onda; não muda o nível das fichas.
- Recursos exclusivos: nenhum registrado.

## Arquivos protegidos

- Instruções e ferramentas de agente: `AGENTS.md`, `CLAUDE.md`, `.claude/` e `.codex/`.
- Instruções da pipeline: `pipeline/`, exceto `pipeline/padroes.md`, `pipeline/particularidades.md` e `pipeline/impactos/`.
- Repositório: `.gitattributes`.
- Configuração protegida nova: ao criá-la ou adotá-la, registre seu caminho real aqui e inclua a regra correspondente em `.claude/settings.json` na mesma entrega, antes de delegar alterações posteriores.
