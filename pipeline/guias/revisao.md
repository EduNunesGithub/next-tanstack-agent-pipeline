# Revisão

> Para: orquestrador · Leia quando: a mudança tem sinal de risco.

Os sinais de risco estão em `papeis/orquestrador.md › 6. Revise`. O que o revisor faz e como responde está em `papeis/revisor.md`.

## Quando

- Por padrão, um único revisor para o conjunto, depois de integrar todas as missões e passar as checagens completas. Não chame um revisor por missão nem por relato.
- Revisão antecipada: obrigatória para o marco arriscado que outras missões vão replicar (`guias/paralelismo.md › Marcos`). Livre em outra necessidade concreta, como validar um contrato antes das missões que dependem dele, ou quando o pedido exige. O motivo vai na entrega.
- A revisão antecipada não conta nos dois ciclos de `Ciclos`: eles são da revisão do conjunto.

## Brief

- O revisor é sempre uma instância nova: nunca um fork desta conversa nem a continuação de outro revisor.
- O brief traz só o que está no modelo.
- Nunca traz missões, raciocínio ou resumo da implementação.
  - Por quê: o valor do revisor está em julgar a mudança sem herdar as suposições de quem a fez.

```markdown
Objetivo: <o que o humano pediu, como resultado>
Critérios: <o que precisa valer, vindo do pedido, das respostas e do que o objetivo implica>
Decisões: <as que você tomou onde o pedido não dizia nada, inclusive mudança em arquivo protegido, cada uma com o motivo>
Base: <referência acessível à base, ou o diff exclusivo da mudança, com arquivos novos e apagados>
Arquivos da tarefa: <só quando o working tree tem outras mudanças>
Achados anteriores: <só no segundo ciclo>
```

## Ciclos

Uma tarefa tem no máximo dois ciclos:

1. **Primeiro:** revisão completa do conjunto.
2. **Segundo:** só se houve correção de achado crítico ou correção substancial, que mudou lógica ou contrato e não só texto, estilo ou nome. Um revisor novo recebe os `Achados anteriores` e uma `Base` no estado revisado, e confere só os achados e as correções.

- Antes de mandar corrigir os achados de um ciclo, guarde o estado revisado: ele é a base do ciclo seguinte.
- Não há terceiro ciclo. O que sobrar do segundo:
  - achado crítico → a correção segue a causa, como no primeiro ciclo, e quem a confirma é você: reproduza a evidência do achado e rode as checagens. Se a correção falhar, siga `guias/falhas.md` até a entrega parcial.
  - achado de consistência → vai para `backlog.md`.
- Revisão sem veredito (`Incompleta:`) não conta como ciclo: chame um revisor novo uma vez. Se de novo não terminar, diga na entrega.

## Achados

Trate cada achado nesta ordem:

1. **Confirme.** Reproduza ou siga o código. Achado sem base (hipotético, preferência, lacuna de checagem) é descartado sem repassar.
2. **Classe.** Mantenha a do revisor ou reclassifique com motivo, pelas definições de `papeis/revisor.md › Classe`.
3. **Escopo.**
   - No que a tarefa mudou: é corrigido nesta tarefa. Depois do último ciclo, siga `Ciclos`.
   - Em código que a tarefa não tocou, inclusive o que veio em `Fora do escopo:`: vai para `backlog.md` e não bloqueia a entrega. Se for crítico, corrigi-lo agora amplia o escopo: é pergunta, levada na entrega com a sua recomendação.
   - Legado de `Fora do escopo:` que o `Legado:` da regra não lista: acrescente (`guias/evolucao.md › Legado sinalizado`).
4. **Causa.** Classifique por `guias/falhas.md › Causa`. O campo `Pipeline:` do achado é indício de causa `pipeline`, não prova: confira o trecho citado.
5. **Correção**, pela causa: `guias/falhas.md › Nova tentativa`.
