# React

## Regras

### R1 · Pasta própria

Componente, contexto e hook ficam numa pasta própria, com a entrada em `<nome>/index.tsx` quando há JSX e em `<nome>/index.ts` nos demais casos.

- Porque: cada unidade tem endereço previsível e mantém os seus arquivos juntos.
- Exceto: arquivo de entrada cujo nome o framework exige mantém esse nome.

### R2 · Um componente por arquivo

Um arquivo define no máximo um componente React. O subcomponente fica numa subpasta do pai, em `<pai>/<filho>/`, com a entrada conforme R1.

- Porque: responsabilidades separadas, e a relação entre componentes visível na árvore de pastas.

### R3 · Pasta só com a entrada e o teste

A pasta de um componente, hook ou contexto contém diretamente só o arquivo de entrada e, quando há, o arquivo de testes da unidade.

- Porque: a unidade continua fácil de achar e não acumula auxiliares soltos.
- Como: utilitários, hooks, contextos, schemas, tipos, constantes e demais auxiliares vão para pastas próprias, conforme a responsabilidade e o alcance de uso. Subpastas são permitidas; subcomponentes seguem R2.

### R4 · Estado mínimo

Estado React guarda só o que não se deriva de props ou de dados existentes, não vem de um recurso da plataforma e não é gerenciado pela biblioteca adotada. Cada dado tem uma única fonte de verdade.

- Porque: menos sincronização, menos renderização à toa e nenhuma divergência entre cópias, com a interação robusta e simples.
- Como:
  - Não duplique valor derivável nem use efeito para mantê-lo sincronizado.
  - Estado React continua certo quando a interação precisa persistir entre renderizações e atualizar a interface. Preserve a reatividade que o comportamento exige.
  - Extrair para hook ou contexto organiza a responsabilidade, mas não justifica criar nem duplicar estado.

## Moldes

Nenhum.

## Alertas

Nenhum.
