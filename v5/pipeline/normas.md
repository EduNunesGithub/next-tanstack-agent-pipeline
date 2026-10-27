# Normas

## Escrita do código

### COD-1: Ordenar alfabeticamente tudo cuja ordem não afete a lógica.

- Por quê: manter a organização consistente e facilitar a localização de elementos.
- Escopo: o código e os arquivos de configuração, inclusive os da raiz: imports, exports, declarações independentes, propriedades, chaves, listas e demais elementos que possam ser reordenados sem alterar o comportamento.
- Como: imports de pacotes externos antes dos internos.
- Exceção: preserve a ordem necessária à execução, às dependências, à precedência ou a qualquer outro significado lógico; não reordene quando isso mudar o resultado. Classes Tailwind seguem a ordem oficial do Tailwind.

### COD-2: Não escrever comentários no código.

- Por quê: manter o código compreensível por seus nomes e estrutura, com explicações na documentação.
- Escopo: comentários de linha ou bloco, comentários de documentação (como JSDoc e docstrings usados como documentação) e código comentado.
- Como: explicações necessárias ficam em arquivos de documentação, fora do código.

### COD-3: Importações de arquivos internos usam os aliases configurados para o ambiente de execução; caminhos relativos são proibidos.

- Por quê: manter as importações consistentes e independentes da localização do arquivo que importa.
- Escopo: o código e as configurações autorais: importações estáticas, reexportações, `import()` e `require()`. Pacotes externos continuam sendo importados pelo nome do pacote.

### COD-4: Componentes, contextos e hooks ficam em pastas próprias, com entrada em `/<nome>/index.tsx` quando houver JSX e `/<nome>/index.ts` nos demais casos.

- Por quê: dar a cada unidade um local previsível e manter seus arquivos relacionados juntos.
- Exceção: arquivos de entrada com nomes exigidos pelo framework preservam esses nomes.

### COD-5: Cada arquivo define no máximo um componente React; componentes filhos ficam em subpastas do componente pai, em `/<nome-componente>/<nome-subcomponente>/`, com entrada conforme COD-4.

- Por quê: manter as responsabilidades separadas e a relação entre os componentes explícita na estrutura de pastas.

### COD-6: Testes unitários ficam na mesma pasta do código testado, em arquivos `*.test.ts` ou `*.test.tsx`.

- Por quê: manter implementação e testes próximos e facilitar sua manutenção conjunta.

### COD-7: A pasta de cada componente, hook ou contexto contém diretamente apenas seu arquivo de entrada e, quando houver testes, um arquivo de testes da unidade.

- Por quê: manter cada unidade fácil de localizar e impedir o acúmulo de arquivos auxiliares sem organização.
- Como: utilitários, hooks, contextos, schemas, tipos, constantes e outros auxiliares ficam em pastas próprias, conforme sua responsabilidade e seu escopo de uso. Subpastas são permitidas; subcomponentes seguem COD-5.

### COD-8: Cada unidade (componente, hook, contexto ou módulo) tem uma única responsabilidade; lógica que dificulte compreender ou manter a unidade é extraída para uma unidade própria.

- Por quê: preservar a simplicidade da implementação e facilitar reutilização, testes e manutenção.
- Como:
  - Quando a coordenação de estados ou comportamentos tornar a unidade complexa, extraia responsabilidades coesas para hooks, contextos ou módulos apropriados, com contratos claros.
  - A concisão preserva nomes expressivos e fluxos fáceis de seguir; abstrações precisam simplificar o uso e a manutenção.

### COD-9: Estado React só guarda o que não pode ser derivado de props ou de dados existentes, nem obtido por um recurso da plataforma, nem gerenciado pela biblioteca já adotada; cada dado tem uma única fonte de verdade.

- Por quê: reduzir sincronização, renderizações desnecessárias e inconsistências, mantendo a interação robusta e simples.
- Como:
  - Não duplique valores deriváveis nem use efeitos para mantê-los sincronizados.
  - Estado React continua adequado quando a interação exige persistência entre renderizações e atualização da interface; preserve a reatividade necessária ao comportamento.
  - Extrair para hook ou contexto organiza a responsabilidade, mas não justifica acrescentar ou duplicar estado.

### COD-10: Reaproveitar o que já existe; duas definições da mesma regra ou do mesmo formato são proibidas.

- Por quê: com uma única fonte por regra, uma mudança vale em todo lugar e nada diverge em silêncio.
- Como:
  - Antes de criar schema, tipo, constante, utilitário, componente, hook ou módulo, procure no projeto e nas bibliotecas adotadas algo que já cumpra o papel.
  - Formato parecido é derivado da fonte (`pick`, `omit`, `extend`, `z.infer`, `z.input`, `z.output`, tipos inferidos do Drizzle e do Better Auth), não reescrito.

### COD-11: Variáveis de ambiente são lidas só no módulo que as valida; `process.env` é proibido fora dele.

- Por quê: ter segurança em tempo de execução e tipagem, e falhar ao subir em vez de no meio de uma requisição.
- Exceção: configurações de ferramenta que não carregam a aplicação, como `playwright.config.ts`.
- Fonte: o caminho do módulo fica em `projeto.md`.

## Interface

### UI-1: Primitivos de interface usam Base UI sempre que houver um componente equivalente, inclusive para controles nativos como botões.

- Por quê: manter comportamento e acessibilidade consistentes.

### UI-2: Transições de componentes Base UI priorizam os mecanismos documentados da biblioteca; outros movimentos usam Motion quando compatível.

- Por quê: preservar o ciclo de vida dos componentes e evitar soluções concorrentes.
- Como: na integração, preservar foco, eventos e montagem/desmontagem; respeitar a preferência por movimento reduzido.

### UI-3: Medidas fixas de layout, espaçamento, raios e comprimentos das sombras são múltiplos de 4px.

- Por quê: manter uma escala visual consistente, mesmo quando o design fornecido usar outra.
- Escopo: a tipografia segue UI-6.
- Exceção: casos técnicos pontuais, como bordas finas, decididos por necessidade e justificados na entrega.

### UI-4: A opacidade das cores usa múltiplos de 0,1 (10%).

- Por quê: manter uma escala previsível de transparência.

### UI-5: Durações e atrasos usam múltiplos de 0,25s (250ms), incluindo zero.

- Por quê: manter o ritmo consistente entre transições, animações e demais temporizações.

### UI-6: A tipografia é definida na fonte global de estilos ou tema adotada no projeto, por elemento semântico ou classe de contexto, usando tokens oficiais de tamanho do Tailwind e suas alturas de linha.

- Por quê: permitir ajustes globais e manter o texto previsível.
- Como:
  - Não usar tamanhos avulsos, alturas de linha manuais ou sobrescritas locais de tamanho e altura.
  - O espaçamento entre letras usa os tokens oficiais `tracking-*` do Tailwind; não usar `letter-spacing` avulso.
- Fonte: o caminho da fonte efetivamente adotada fica em `projeto.md`; a configuração segue a versão instalada.

### UI-7: O espaçamento entre elementos usa `gap` no contêiner.

- Por quê: tornar a separação explícita e facilitar a depuração visual.
- Como: não usar margens ou `space-*` para esse fim; `padding` define o espaço interno.

### UI-8: Classes Tailwind ficam inline em `className`, inclusive nas chamadas a `twMerge` e nas expressões que ramificam a aparência, sempre que possível.

- Por quê: preservar o autocomplete do Tailwind CSS e manter a aparência visível junto do elemento que ela estiliza.

### UI-9: Ícones da interface usam `lucide-react`.

- Por quê: manter uma linguagem visual consistente e evitar recriar os símbolos fornecidos pela biblioteca.

### UI-10: Classes compostas de mais de uma parte (condicionais, props ou variáveis) são combinadas com `twMerge`; não concatenar classes com template literal, `+` ou `join`.

- Por quê: resolver conflitos entre utilidades de forma previsível e manter uma única forma de compor classes.
