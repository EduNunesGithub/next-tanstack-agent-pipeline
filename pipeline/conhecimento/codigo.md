# Código

> Para: todos os papéis · Leia quando: sempre que se escreve ou revisa um arquivo autoral.

## Fontes

- Nenhuma registrada. Entram aqui, conferidos no destino, a configuração dos aliases de importação (COD-3) e o módulo que valida as variáveis de ambiente (COD-11).

## Regras

### COD-1: Ordenar alfabeticamente tudo cuja ordem não tem significado.

- Por quê: com uma ordem única e previsível, qualquer elemento se acha sem procurar, e o diff mostra só o que mudou.
- Escopo: código e arquivos de configuração autorais, inclusive os da raiz: imports, exports, declarações independentes, propriedades, chaves, membros de listas e de uniões, e todo elemento que se reordena sem mudar o comportamento.
- Como: imports de pacotes externos antes dos internos.
- Exceção: mantenha a ordem que carrega significado lógico. Contam como significado a ordem de execução, a dependência entre declarações que a execução exige (uma constante que usa outra ao ser inicializada; função declarada, que a linguagem eleva, não conta), a precedência (cascata de estilos, middlewares), a ordem de exibição ao usuário (itens de menu, campos de formulário, colunas, etapas) e a ordem exigida por uma ferramenta. Classes Tailwind seguem a ordem oficial do Tailwind.

### COD-2: Não escrever comentários no código.

- Por quê: o código se explica pelos nomes e pela estrutura; a explicação que ainda faltar mora na documentação.
- Escopo: comentário de linha e de bloco, comentário de documentação (JSDoc, docstring) e código comentado.
- Como: a explicação necessária vai para um arquivo de documentação, fora do código.

### COD-3: Importações internas usam os aliases configurados para o ambiente de execução do arquivo; caminho relativo é proibido.

- Por quê: o import não depende de onde está o arquivo que importa, e mover um arquivo não quebra os vizinhos.
- Escopo: código e configuração autorais: import estático, reexportação, `import()` e `require()`. Pacote externo continua importado pelo nome.
- Fonte: a configuração dos aliases, em `Fontes`.

### COD-4: Componente, contexto e hook ficam numa pasta própria, com a entrada em `<nome>/index.tsx` quando há JSX e em `<nome>/index.ts` nos demais casos.

- Por quê: cada unidade tem endereço previsível e mantém os seus arquivos juntos.
- Exceção: arquivo de entrada cujo nome o framework exige mantém esse nome.

### COD-5: Um arquivo define no máximo um componente React; o subcomponente fica numa subpasta do pai, em `<pai>/<filho>/`, com a entrada conforme COD-4.

- Por quê: responsabilidades separadas e a relação entre componentes visível na árvore de pastas.

### COD-6: O teste unitário fica na pasta do código que ele testa, em `*.test.ts` ou `*.test.tsx`.

- Por quê: implementação e teste se acham juntos e mudam juntos.

### COD-7: A pasta de um componente, hook ou contexto contém diretamente só o arquivo de entrada e, quando há, o arquivo de testes da unidade.

- Por quê: a unidade continua fácil de achar e não acumula auxiliares soltos.
- Como: utilitários, hooks, contextos, schemas, tipos, constantes e demais auxiliares vão para pastas próprias, conforme a responsabilidade e o alcance de uso. Subpastas são permitidas; subcomponentes seguem COD-5.

### COD-8: Cada unidade (componente, hook, contexto ou módulo) tem uma única responsabilidade; lógica que dificulta entender ou manter a unidade vira uma unidade própria.

- Por quê: implementação simples, fácil de reutilizar, testar e manter.
- Como:
  - Quando coordenar estados ou comportamentos deixa a unidade complexa, extraia responsabilidades coesas para hooks, contextos ou módulos, com contrato claro.
  - Concisão não sacrifica nome expressivo nem fluxo fácil de seguir; uma abstração só entra se simplifica o uso e a manutenção.

### COD-9: Estado React guarda só o que não se deriva de props ou de dados existentes, não vem de um recurso da plataforma e não é gerenciado pela biblioteca adotada; cada dado tem uma única fonte de verdade.

- Por quê: menos sincronização, menos renderização à toa e nenhuma divergência entre cópias, com a interação robusta e simples.
- Como:
  - Não duplique valor derivável nem use efeito para mantê-lo sincronizado.
  - Estado React continua certo quando a interação precisa persistir entre renderizações e atualizar a interface; preserve a reatividade que o comportamento exige.
  - Extrair para hook ou contexto organiza a responsabilidade, mas não justifica criar nem duplicar estado.

### COD-10: Reaproveitar o que já existe; a mesma regra ou o mesmo formato nunca tem duas definições.

- Por quê: com uma fonte por regra, uma mudança vale em todo lugar e nada diverge em silêncio.
- Como:
  - Antes de criar schema, tipo, constante, utilitário, componente, hook ou módulo, procure no projeto e nas bibliotecas adotadas algo que já cumpra o papel.
  - Formato parecido deriva da fonte (`pick`, `omit`, `extend`, `z.infer`, `z.input`, `z.output`, tipos inferidos do Drizzle e do Better Auth); não é reescrito.

### COD-11: Variável de ambiente é lida só no módulo que a valida; `process.env` é proibido fora dele.

- Por quê: segurança e tipos em tempo de execução, e a falha aparece ao subir a aplicação, não no meio de uma requisição.
- Exceção: configuração de ferramenta que não carrega a aplicação, como `playwright.config.ts`.
- Fonte: o módulo de validação, em `Fontes`.

### COD-12: Identificadores do código em inglês; documentação em português do Brasil.

- Por quê: um idioma por destino evita nomes misturados e mantém a documentação legível para quem mantém o projeto.
- Escopo: identificadores são os nomes no código (variáveis, funções, tipos, componentes, chaves). Documentação são os arquivos de texto para pessoas, como `.md`. O texto exibido na interface segue UI-11.
- Exceção: nome imposto por uma ferramenta ou por um contrato externo.

### COD-13: Arquivos e pastas autorais têm nome em kebab-case.

- Por quê: um formato único de nome mantém os caminhos previsíveis e evita colisão entre sistemas que diferenciam maiúsculas de minúsculas e os que não diferenciam.
- Exceção: nome exigido por ferramenta, framework ou convenção do ecossistema, como `page.tsx`, `README.md` e `AGENTS.md`.

## Padrões

- Nenhum registrado.

## Armadilhas

- Nenhuma registrada.
