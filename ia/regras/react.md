# React

## Regras

### R2 · Um componente por arquivo

Um arquivo define no máximo um componente React. O subcomponente fica numa subpasta do pai, em `<pai>/<filho>/`, conforme `ia/regras/codigo.md › C11`.

- Porque: responsabilidades separadas, e a relação entre componentes visível na árvore de pastas.

### R4 · Estado mínimo

Estado React guarda só o que não se deriva de props ou de dados existentes, não vem de um recurso da plataforma e não é gerenciado pela biblioteca adotada. Cada dado tem uma única fonte de verdade.

- Porque: menos sincronização, menos renderização à toa e nenhuma divergência entre cópias, com a interação robusta e simples.
- Como:
  - Não duplique valor derivável nem use efeito para mantê-lo sincronizado.
  - Estado que precisa sobreviver a recarga ou a link compartilhado (filtro, aba, página, ordenação, item aberto) mora na URL.
  - Estado React continua certo quando a interação precisa persistir entre renderizações e atualizar a interface. Preserve a reatividade que o comportamento exige.
  - Extrair para hook ou contexto organiza a responsabilidade, mas não justifica criar nem duplicar estado.

### R5 · Efeito e estado coordenado em hook próprio

Componente não chama `useEffect`, `useLayoutEffect`, `useSyncExternalStore` nem `useReducer` direto: cada um mora num hook com nome, em pasta própria, que devolve só o que o componente usa.

- Porque: efeito, assinatura e máquina de estado são a lógica que mais fica presa em componente; num hook, ganham nome, teste e um lugar só.
- Vale para: também o mesmo conjunto de estado e manipuladores repetido em dois componentes.
- Como: antes de escrever o efeito, confira R4: valor derivado e reação a evento do usuário não pedem efeito.
- Exceto: `useState` e manipuladores usados num componente só ficam nele.
