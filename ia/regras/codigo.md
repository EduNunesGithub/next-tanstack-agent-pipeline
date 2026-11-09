# Código

## Regras

### C1 · Ordem alfabética

Ordene alfabeticamente tudo cuja ordem não tem significado.

- Porque: com uma ordem única, qualquer elemento se acha sem procurar, e o diff mostra só o que mudou.
- Vale para: código e configuração autorais, inclusive na raiz: imports, exports, declarações independentes, propriedades, chaves, membros de listas e de uniões, e tudo o que se reordena sem mudar o comportamento.
- Como: imports de pacotes externos antes dos internos.
- Exceto: ordem com significado lógico:
  - a ordem de execução;
  - a dependência que a execução exige, como uma constante que usa outra ao ser inicializada. Função declarada, que a linguagem eleva, não conta;
  - a precedência, como cascata de estilos e middlewares;
  - a ordem de exibição ao usuário, como itens de menu, campos de formulário, colunas e etapas;
  - a ordem que uma ferramenta exige. Classes Tailwind seguem a ordem oficial do Tailwind.

### C2 · Sem comentários

Não escreva comentários no código.

- Porque: o código se explica pelos nomes e pela estrutura; a explicação que faltar mora na documentação.
- Vale para: comentário de linha e de bloco, comentário de documentação (JSDoc, docstring) e código comentado.
- Como: a explicação necessária vai para um arquivo de documentação, fora do código.

### C3 · Imports por alias

Importação interna usa o alias configurado para o ambiente de execução do arquivo. Caminho relativo é proibido.

- Porque: o import não depende de onde está o arquivo que importa, e mover um arquivo não quebra os vizinhos.
- Vale para: código e configuração autorais: import estático, reexportação, `import()` e `require()`. Pacote externo continua importado pelo nome.
- Fonte: a configuração dos aliases. Registre o caminho aqui quando ela existir.

### C4 · Teste ao lado do código

O teste unitário fica na pasta do código que ele testa, em `*.test.ts` ou `*.test.tsx`.

- Porque: implementação e teste se acham juntos e mudam juntos.

### C5 · Uma responsabilidade por unidade

Cada unidade (componente, hook, contexto ou módulo) tem uma única responsabilidade. Lógica que dificulta entender ou manter a unidade vira uma unidade própria.

- Porque: implementação simples, fácil de reutilizar, testar e manter.
- Como:
  - Quando coordenar estados ou comportamentos deixa a unidade complexa, extraia responsabilidades coesas para hooks, contextos ou módulos, com contrato claro.
  - Concisão não sacrifica nome expressivo nem fluxo fácil de seguir. Uma abstração só entra se simplifica o uso e a manutenção.

### C6 · Uma definição só

Reaproveite o que já existe. A mesma regra ou o mesmo formato nunca tem duas definições.

- Porque: com uma fonte por regra, uma mudança vale em todo lugar e nada diverge em silêncio.
- Como:
  - Antes de criar schema, tipo, constante, utilitário, componente, hook ou módulo, procure no projeto e nas bibliotecas adotadas algo que já cumpra o papel.
  - Formato parecido deriva da fonte (`pick`, `omit`, `extend`, `z.infer`, `z.input`, `z.output`, tipos inferidos do Drizzle e do Better Auth). Não é reescrito.

### C7 · Ambiente num módulo só

Variável de ambiente é lida só no módulo que a valida. `process.env` é proibido fora dele.

- Porque: segurança e tipos em tempo de execução, e a falha aparece ao subir a aplicação, não no meio de uma requisição.
- Exceto: configuração de ferramenta que não carrega a aplicação, como `playwright.config.ts`.
- Fonte: o módulo de validação. Registre o caminho aqui quando ele existir.

### C8 · Idioma

Identificadores do código em inglês. Documentação em português do Brasil.

- Porque: um idioma por destino evita nomes misturados e mantém a documentação legível para quem mantém o projeto.
- Vale para: identificadores são os nomes no código (variáveis, funções, tipos, componentes, chaves). Documentação são os arquivos de texto para pessoas, como `.md`. Texto exibido na interface: `ia/regras/visual.md › V11`.
- Exceto: nome imposto por uma ferramenta ou por um contrato externo.

### C9 · Nomes em kebab-case

Arquivos e pastas autorais têm nome em kebab-case.

- Porque: um formato único mantém os caminhos previsíveis e evita colisão entre sistemas que diferenciam maiúsculas de minúsculas e os que não diferenciam.
- Exceto: nome exigido por ferramenta, framework ou convenção do ecossistema, como `page.tsx`, `README.md` e `AGENTS.md`.

## Moldes

Nenhum.

## Alertas

Nenhum.
