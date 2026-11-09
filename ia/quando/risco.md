# Risco

A mudança tem sinal de risco (`ia/fluxo.md › 5. Valide`): chame um auditor.

## Quando

- Uma auditoria só, do conjunto, depois de integrar tudo e passar as checagens completas. Nunca uma por encomenda.
- Antecipada: obrigatória para o marco arriscado que outras encomendas vão replicar (`ia/quando/paralelo.md › Marcos`). Livre para outra necessidade concreta, como validar um fixo antes de quem depende dele. O motivo vai na entrega.
- A antecipada não conta em `Ciclos`.

## Pedido de auditoria

- O auditor é sempre uma instância nova: nunca um fork desta conversa nem a continuação de outro auditor.
- O pedido traz só o modelo abaixo. Nunca encomendas, raciocínio ou resumo da implementação.
  - Porque: o valor do auditor está em julgar sem herdar as suposições de quem fez.

```markdown
Objetivo: <o que o humano pediu, como resultado>
Critérios: <o que precisa valer: do pedido, das respostas e do que o objetivo implica>
Escolhas: <as que você fez onde o pedido não dizia nada, inclusive protegido alterado, com o motivo>
Base: <referência à base, ou o diff só da mudança, com arquivos novos e apagados>
Arquivos: <só quando o working tree tem outras mudanças>
Achados anteriores: <só no segundo ciclo>
```

## Ciclos

No máximo dois por tarefa:

1. Auditoria completa do conjunto.
2. Só se houve correção de `quebra`, ou correção que mudou lógica ou fixo. Um auditor novo recebe os `Achados anteriores` e a `Base` no estado auditado.

- Antes de mandar corrigir, guarde o estado auditado: é a base do ciclo seguinte.
- Não há terceiro ciclo. O que sobrar do segundo:
  - `quebra`: corrija pela causa e confirme você mesmo, reproduzindo a evidência e rodando as checagens. Não resolveu: `ia/quando/falha.md`.
  - `destoa`: vai para `ia/pendencias.md`.
- `Inconclusivo:` não conta como ciclo. Chame um auditor novo uma vez; se repetir, diga na entrega.

## Achados

Trate cada um nesta ordem:

1. **Confirme.** Reproduza ou siga o código. Sem base (hipotético, preferência, lacuna de checagem): descarte.
2. **Classe.** Mantenha ou reclassifique com motivo (`ia/auditor.md › Procure`).
3. **Escopo.**
   - No que a tarefa mudou: corrija nesta tarefa.
   - No que a tarefa não tocou, inclusive `De passagem:`: vai para `ia/pendencias.md` e não bloqueia. Se for `quebra`, é pergunta na entrega, com recomendação.
4. **Causa e correção.** `ia/quando/falha.md`. O campo `Pipeline:` é indício de causa `pipeline`, não prova: confira o trecho.
