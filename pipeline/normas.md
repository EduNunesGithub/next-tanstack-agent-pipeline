# Normas

> Os limites que não podem variar neste projeto. Só muda com aprovação do humano, que normalmente vem junto com a entrega que motivou a mudança.

Uma norma:

- diz o que é obrigatório ou proibido, e por quê;
- é verificável olhando o código;
- aponta para a fonte da verdade (schema, tema, constantes) em vez de copiar o conteúdo dela;
- vale para o código do produto e, quando a norma indicar, para arquivos de configuração, respeitando a semântica das ferramentas;
- só existe se, sem ela, um agente competente que lê o código decidiria pior.

Se uma funcionalidade comum exige reescrever uma norma, a norma está descrevendo implementação: reescreva-a como limite. Exemplos do que cumpre ou viola só entram quando ajudam. `Legado:` aponta o código que ainda não cumpre a norma e sai quando não houver mais nenhum. Um ID removido não é reaproveitado.

Formato:

```markdown
### <ID>: <obrigação ou proibição verificável>

Por quê: <motivo do limite>
Fonte: <referência existente, quando necessária>
Legado: <caminho conferido que ainda descumpre a norma, se houver>
```

<!-- As normas do projeto entram abaixo, agrupadas por área quando forem várias. -->

## Escrita do código

### COD-1: Ordenar alfabeticamente tudo cuja ordem não afete a lógica.

Por quê: manter a organização consistente e facilitar a localização de elementos.
Aplica-se ao código e aos arquivos de configuração, inclusive os da raiz: imports, exports, declarações independentes, propriedades, chaves, listas e demais elementos que possam ser reordenados sem alterar o comportamento.
Preserve a ordem necessária à execução, às dependências, à precedência ou a qualquer outro significado lógico; não reordene quando isso mudar o resultado.
Classes Tailwind seguem a ordenação oficial, pela integração compatível com a versão adotada.

### COD-2: Não escrever comentários no código.

Por quê: manter o código compreensível por seus nomes e estrutura, com explicações na documentação.
Inclui comentários de linha ou bloco, comentários de documentação (como JSDoc e docstrings usados como documentação) e código comentado. Explicações necessárias ficam em arquivos de documentação, fora do código.

### COD-3: Importações de arquivos internos usam os aliases configurados para o ambiente de execução; caminhos relativos são proibidos.

Por quê: manter as importações consistentes e independentes da localização do arquivo que importa.
Aplica-se ao código e às configurações autorais: importações estáticas, reexportações, `import()` e `require()`. Pacotes externos continuam sendo importados pelo nome do pacote.

### COD-4: Componentes, contextos e hooks ficam em pastas próprias, com entrada em `/<nome>/index.tsx` quando houver JSX e `/<nome>/index.ts` nos demais casos.

Por quê: dar a cada unidade um local previsível e manter seus arquivos relacionados juntos.
Arquivos de entrada com nomes exigidos pelo framework preservam esses nomes.

### COD-5: Cada arquivo define no máximo um componente React; componentes filhos ficam em subpastas do componente pai, em `/<nome-componente>/<nome-subcomponente>/`, com entrada conforme COD-4.

Por quê: manter as responsabilidades separadas e a relação entre os componentes explícita na estrutura de pastas.

### COD-6: Testes unitários ficam na mesma pasta do código testado, em arquivos `*.test.ts` ou `*.test.tsx`.

Por quê: manter implementação e testes próximos e facilitar sua manutenção conjunta.

### COD-7: A pasta de cada componente, hook ou contexto contém diretamente apenas seu arquivo de entrada e, quando houver testes, um arquivo de testes da unidade.

Por quê: manter cada unidade fácil de localizar e impedir o acúmulo de arquivos auxiliares sem organização.
Utilitários, hooks, contextos, schemas, tipos, constantes e outros auxiliares ficam em pastas próprias, conforme sua responsabilidade e seu escopo de uso. Subpastas são permitidas; subcomponentes seguem COD-5.

### COD-8: Escrever código compacto, legível e com responsabilidades bem definidas; extrair lógica que dificulte compreender ou manter a unidade.

Por quê: preservar a simplicidade da implementação e facilitar reutilização, testes e manutenção.
Quando a coordenação de estados ou comportamentos tornar a unidade complexa, extraia responsabilidades coesas para hooks, contextos ou módulos apropriados, com contratos claros. A concisão preserva nomes expressivos e fluxos fáceis de seguir; abstrações precisam simplificar o uso e a manutenção.

### COD-9: Usar o mínimo de estado React necessário, com uma única fonte de verdade para cada dado.

Por quê: reduzir sincronização, renderizações desnecessárias e inconsistências, mantendo a interação robusta e simples.
Antes de criar estado, verifique se o valor pode ser derivado de props ou dados existentes, obtido por um recurso da plataforma ou gerenciado pela biblioteca já adotada. Não duplique valores deriváveis nem use efeitos para mantê-los sincronizados. Estado React continua adequado quando a interação exige persistência entre renderizações e atualização da interface; preserve a reatividade necessária ao comportamento. Extrair para hook ou contexto organiza a responsabilidade, mas não justifica acrescentar ou duplicar estado.

## Interface

### UI-1: Primitivos de interface usam Base UI sempre que houver um componente equivalente, inclusive para controles nativos como botões.

Por quê: manter comportamento e acessibilidade consistentes.

### UI-2: Transições de componentes Base UI priorizam os mecanismos documentados da biblioteca; outros movimentos usam Motion quando compatível.

Por quê: preservar o ciclo de vida dos componentes e evitar soluções concorrentes.
Na integração, preservar foco, eventos e montagem/desmontagem; respeitar a preferência por movimento reduzido.

### UI-3: Medidas fixas de layout, espaçamento, raios e comprimentos das sombras são múltiplos de 4px.

Por quê: manter uma escala visual consistente, mesmo quando o design fornecido usar outra.
Exceções técnicas pontuais, como bordas finas, são decididas por necessidade e justificadas na entrega. A tipografia segue UI-6.

### UI-4: A opacidade das cores usa múltiplos de 0,1 (10%).

Por quê: manter uma escala previsível de transparência.

### UI-5: Durações e atrasos usam múltiplos de 0,25s (250ms), incluindo zero.

Por quê: manter o ritmo consistente entre transições, animações e demais temporizações.

### UI-6: A tipografia é definida na fonte global de estilos ou tema adotada no projeto, por elemento semântico ou classe de contexto, usando tokens oficiais de tamanho do Tailwind e suas alturas de linha.

Por quê: permitir ajustes globais e manter o texto previsível.
O caminho da fonte efetivamente adotada fica em `projeto.md`; a configuração segue a versão instalada.
Não usar tamanhos avulsos, alturas de linha manuais ou sobrescritas locais de tamanho e altura.

### UI-7: O espaçamento entre elementos usa `gap` no contêiner.

Por quê: tornar a separação explícita e facilitar a depuração visual.
Não usar margens ou `space-*` para esse fim; `padding` define o espaço interno.

### UI-8: Classes Tailwind ficam inline em `className`, inclusive nas chamadas a `twMerge` e nas expressões que ramificam a aparência, sempre que possível.

Por quê: preservar o autocomplete do Tailwind CSS e manter a aparência visível junto do elemento que ela estiliza.

### UI-9: Ícones da interface usam `lucide-react`.

Por quê: manter uma linguagem visual consistente e evitar recriar os símbolos fornecidos pela biblioteca.
