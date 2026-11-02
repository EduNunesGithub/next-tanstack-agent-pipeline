# Configuração

> Para: todos os papéis · Leia quando: arquivo de configuração de ferramenta ou em `eslint-rules/`, ou instalar ou remover uma dependência.

## Fontes

- Nenhuma registrada.

## Regras

### CFG-1: Arquivo de configuração de ferramenta escrito em JavaScript usa a extensão `.mjs`, nunca `.js`.

- Por quê: a extensão declara o arquivo como módulo ES sem depender do campo `type` do `package.json`, e toda ferramenta o carrega do mesmo jeito.
- Exceção:
  - `.ts`, quando a versão instalada da ferramenta carrega configuração em TypeScript pela documentação oficial dela;
  - a extensão que a ferramenta exige, quando ela não carrega `.mjs`.

### CFG-2: O `export default` de um arquivo de configuração exporta uma constante declarada antes, nunca o valor direto.

- Por quê: a configuração ganha um nome, que pode receber o tipo da ferramenta, e todo arquivo de configuração tem a mesma forma.
- Escopo: arquivo de configuração de ferramenta e módulo de `eslint-rules/` (CFG-3).
- Como: `const config = { … };` e, depois, `export default config;`. Valor montado por uma função, como `defineConfig(…)`, também vai para a constante.

### CFG-3: Regra customizada do ESLint fica em `eslint-rules/<nome>/`, fora do arquivo de configuração do ESLint, que só importa e compõe.

- Por quê: o arquivo de configuração do ESLint fica limpo, e cada regra customizada tem endereço próprio.
- Escopo: regra customizada é a regra que o projeto escreve, ou a regra existente que o projeto ativa ou ajusta fora das configurações de CFG-4 e CFG-5.
- Como:
  - A entrada é `eslint-rules/<nome>/index.ts` quando o arquivo de configuração do ESLint é `.ts`, e `eslint-rules/<nome>/index.mjs` nos demais casos.
  - Compor é montar a lista das configurações importadas, com os escopos de arquivo, os `ignores` e as opções que a documentação delas pede. Objeto `rules` escrito no próprio arquivo de configuração do ESLint não é composição.

### CFG-4: O ESLint usa o Perfectionist com a configuração recomendada de ordem alfabética, `recommended-alphabetical`.

- Por quê: a ordem de COD-1, no que o Perfectionist cobre, passa a ser conferida e corrigida por uma ferramenta, não só pela revisão.

### CFG-5: Fora o Perfectionist e as regras customizadas, as regras do ESLint vêm só das configurações recomendadas pela documentação oficial de cada tecnologia do projeto.

- Por quê: as regras acompanham quem mantém cada tecnologia e se atualizam com ela, sem uma seleção própria para manter.
- Como:
  - A configuração entra no projeto com a tecnologia (STK-2) e sai com ela.
  - Quando a documentação oficial oferece mais de uma configuração, vale a que ela chama de recomendada.

## Padrões

- Nenhum registrado.

## Armadilhas

- Nenhuma registrada.
