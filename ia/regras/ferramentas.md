# Ferramentas

## Regras

### F1 · Configuração em `.mjs`

Arquivo de configuração de ferramenta escrito em JavaScript usa a extensão `.mjs`, nunca `.js`.

- Porque: a extensão declara o arquivo como módulo ES sem depender do campo `type` do `package.json`, e toda ferramenta o carrega do mesmo jeito.
- Exceto:
  - `.ts`, quando a versão instalada da ferramenta carrega configuração em TypeScript, pela documentação oficial dela;
  - a extensão que a ferramenta exige, quando ela não carrega `.mjs`.

### F2 · Exportação por constante

O `export default` de um arquivo de configuração exporta uma constante declarada antes, nunca o valor direto.

- Porque: a configuração ganha um nome, que pode receber o tipo da ferramenta, e todo arquivo de configuração tem a mesma forma.
- Vale para: arquivo de configuração de ferramenta e módulo de `eslint-rules/` (F3).
- Como: `const config = { … };` e, depois, `export default config;`. Valor montado por uma função, como `defineConfig(…)`, também vai para a constante.

### F3 · Regras customizadas do ESLint em `eslint-rules/`

Regra customizada do ESLint fica em `eslint-rules/<nome>/`, fora do arquivo de configuração do ESLint, que só importa e compõe.

- Porque: o arquivo de configuração do ESLint fica limpo, e cada regra customizada tem endereço próprio.
- Vale para: a regra que o projeto escreve, e a regra existente que o projeto ativa ou ajusta fora das configurações de F4 e F5.
- Como:
  - A entrada é `eslint-rules/<nome>/index.ts` quando o arquivo de configuração do ESLint é `.ts`, e `eslint-rules/<nome>/index.mjs` nos demais casos.
  - Compor é montar a lista das configurações importadas, com os escopos de arquivo, os `ignores` e as opções que a documentação delas pede. Objeto `rules` escrito no próprio arquivo de configuração do ESLint não é composição.

### F4 · Perfectionist alfabético

O ESLint usa o Perfectionist com a configuração recomendada de ordem alfabética, `recommended-alphabetical`.

- Porque: a ordem de `ia/regras/codigo.md › C1`, no que o Perfectionist cobre, passa a ser conferida e corrigida por uma ferramenta, não só pela auditoria.

### F5 · Só configurações recomendadas

Fora o Perfectionist e as regras customizadas, as regras do ESLint vêm só das configurações recomendadas pela documentação oficial de cada tecnologia do projeto.

- Porque: as regras acompanham quem mantém cada tecnologia e se atualizam com ela, sem uma seleção própria para manter.
- Como:
  - A configuração entra no projeto com a tecnologia (`ia/regras/bibliotecas.md › B2`) e sai com ela.
  - Quando a documentação oficial oferece mais de uma configuração, vale a que ela chama de recomendada.

## Moldes

Nenhum.

## Alertas

Nenhum.
