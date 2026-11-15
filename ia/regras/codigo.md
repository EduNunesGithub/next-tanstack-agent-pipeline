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

### C4 · Teste ao lado do código

O teste unitário fica na pasta do código que ele testa, em `*.test.ts` ou `*.test.tsx`.

- Porque: implementação e teste se acham juntos e mudam juntos.

### C5 · Lógica fora da interface

Cada unidade tem uma única responsabilidade. Arquivo de interface (componente, página, layout) só monta a interface: a lógica que se testa sem renderizar sai dele para uma unidade própria, com teste.

- Porque: lógica dentro do componente só se testa renderizando, não se reaproveita e esconde o que a tela faz.
- Vale para (sai do arquivo):
  - função que não devolve JSX, declarada fora ou dentro do componente;
  - cálculo que ocupa mais de uma instrução: laço, `if` ou variável intermediária;
  - regra de negócio e validação, de qualquer tamanho.
- Exceto (fica): expressão única sobre dados prontos, como `map`, `filter` e ternário; manipulador de evento que só chama uma função ou atualiza estado; ramificação de aparência.
- Como:
  - A unidade nasce na subpasta de quem a usa (C11) e só sobe para um lugar compartilhado no segundo uso.
  - Extrair não é generalizar: nenhum parâmetro, opção ou abstração que o uso atual não pede.
  - Lógica com estado ou efeito: `ia/regras/react.md › R5`.

### C6 · Uma definição só

Reaproveite o que já existe. A mesma regra ou o mesmo formato nunca tem duas definições.

- Porque: com uma fonte por regra, uma mudança vale em todo lugar e nada diverge em silêncio.
- Como:
  - Antes de criar schema, tipo, constante, utilitário, componente, hook ou módulo, liste as pastas do projeto (com C11, o nome de cada uma diz o que existe) e confira as bibliotecas adotadas, com os plugins oficiais delas.
  - O que uma biblioteca adotada oferece nunca se reimplementa à mão.
  - Formato parecido deriva da fonte (`pick`, `omit`, `extend`, `z.infer`, `z.input`, `z.output`, tipos inferidos do Drizzle e do Better Auth). Não é reescrito.

### C7 · Ambiente num módulo só

Variável de ambiente é lida só no módulo que a valida. `process.env` é proibido fora dele.

- Porque: segurança e tipos em tempo de execução, e a falha aparece ao subir a aplicação, não no meio de uma requisição.
- Exceto: configuração de ferramenta que não carrega a aplicação, como `playwright.config.ts`.

### C8 · Idioma

Identificadores do código em inglês. Documentação em português do Brasil.

- Porque: um idioma por destino evita nomes misturados e mantém a documentação legível para quem mantém o projeto.
- Vale para: identificadores são os nomes no código (variáveis, funções, tipos, componentes, chaves). Documentação são os arquivos de texto para pessoas, como `.md`. Texto exibido na interface: `ia/regras/visual.md › V11`.
- Exceto: nome imposto por uma ferramenta ou por um contrato externo.

### C9 · Nomes em kebab-case

Arquivos e pastas autorais têm nome em kebab-case.

- Porque: um formato único mantém os caminhos previsíveis e evita colisão entre sistemas que diferenciam maiúsculas de minúsculas e os que não diferenciam.
- Exceto: nome exigido por ferramenta, framework ou convenção do ecossistema, como `page.tsx`, `README.md` e `AGENTS.md`.

### C10 · README só para rodar

O `README.md` diz só o que uma pessoa precisa para instalar, rodar e checar o projeto, e é a única fonte disso. Nunca explica o código nem dá instrução para quem o altera.

- Porque: o que o código mostra não se repete, e o que só agentes precisam mora em `ia/`.

### C11 · Uma unidade por pasta

Uma pasta autoral contém diretamente no máximo dois arquivos: a entrada da unidade, em `index.ts` (`index.tsx` quando há JSX), e o teste dela, em `index.test.ts` (`index.test.tsx`). Toda outra unidade fica numa subpasta própria, com o nome do que ela faz.

- Porque: cada unidade tem endereço previsível, e a árvore de pastas é o catálogo do projeto, sem um índice para manter.
- Vale para: todo código autoral: componentes, hooks, contextos, módulos, scripts, utilitários de teste, schemas, tipos e constantes. Pasta só com subpastas é permitida.
- Como: subpastas demais lado a lado se agrupam em pastas por assunto, sem arquivo próprio.
- Exceto: arquivo cujo nome e lugar o framework ou a ferramenta exigem, como `page.tsx` e `layout.tsx`; configuração na raiz do projeto.
