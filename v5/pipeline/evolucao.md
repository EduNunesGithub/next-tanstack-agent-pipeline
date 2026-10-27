# Evolução da pipeline

> Para o orquestrador: quando a pipeline muda e com que autoridade. Como escrever cada entrada está em `escrita.md`.

Só o orquestrador escreve em `pipeline/`.

## Gatilhos

Avalie uma mudança na pipeline quando acontecer um destes:

1. **Cobertura:** o pedido leva o projeto a terreno que a pipeline não cobre (`orquestracao.md › Cobertura da pipeline`).
2. **Achado com causa `pipeline`** (`orquestracao.md › Causa dos achados`).
3. **Registro do implementador** (seção Registro do implementador, abaixo).
4. **Instrução duradoura do humano:** "a partir de agora, sempre X". Se não está claro que é duradoura, vale só para a tarefa atual.
5. **Atrito:** uma instrução causou retrabalho, pergunta desnecessária ou resíduo, ou o humano reclamou de um comportamento.

## Avalie o impacto

Antes de escrever, responda:

- Sem a entrada, agentes competentes decidiriam de formas diferentes ou erradas? Se não, não escreva nada.
- Qual é o tipo certo? Norma (obrigação ou proibição verificável), padrão (forma a repetir, com exemplar), particularidade (armadilha, limitação ou decisão que o código não explica), convenção ou fonte em `projeto.md`. Os critérios de cada tipo estão em `escrita.md`.
- Que código existente passaria a descumprir a entrada? Que normas, padrões ou decisões registradas ela toca?
- Quais são as alternativas, inclusive não escrever nada, e a consequência de cada uma?

Uma biblioteca nova costuma pedir duas entradas em momentos diferentes:

- uma norma, antes de delegar, que fecha a escolha ("dados tabulares usam TanStack Table");
- um padrão, depois da primeira instância, que registra a forma de uso com o exemplar.

## Aplicar ou propor

### Aplique e declare

- Entrada nova em `normas.md` ou em `projeto.md › Convenções` que seja aditiva e sem conflito (abaixo).
- Entrada nova, alterada ou removida em `padroes.md`, `particularidades.md` e `backlog.md`.
  - Por quê: padrões não são normas; o próprio arquivo prevê o desvio justificado e a atualização da entrada.
- Fato conferido em `projeto.md`: estado de adoção, fontes de referência, checagens, paralelismo, arquivo protegido novo.
- Manutenção de uma norma que não muda o que ela exige: acrescentar o `Checagem:` que a garante, tirar de `Legado:` um caminho que passou a cumprir, atualizar um caminho que mudou de lugar.
- Registro em `impactos/`.

### Proponha e aguarde aprovação

- Alterar ou remover uma norma ou uma convenção existente.
- Entrada nova em `normas.md` ou em `projeto.md › Convenções` que tenha conflito.
- Qualquer mudança em `AGENTS.md`, `CLAUDE.md`, nos arquivos de processo (`orquestracao.md`, `ficha.md`, `revisao.md`, `evolucao.md`, `escrita.md`, `adocao.md`), em `stack.md`, nas definições de agente ou nas configurações de `.claude/` e `.codex/`.
  - Por quê: essas mudanças valem para todas as tarefas seguintes, e um erro nelas se repete em cada uma.
- Tirar um arquivo da lista de protegidos de `projeto.md`.

Exceção: um pedido explícito do humano para mudar uma norma ou instrução ("troque UI-7 por...", "a partir de agora, sempre X") já é a aprovação. Aplique e declare. Conflito entre o pedido e uma norma que o humano não mencionou não é aprovação: é pergunta (`orquestracao.md › Autonomia`).

### Aditiva e sem conflito

Uma entrada nova é aditiva e sem conflito quando todas estas condições valem:

- não contradiz, não restringe e não amplia uma norma, convenção, padrão ou decisão registrada;
- não escolhe entre duas formas que já convivem no código;
- não faz código que hoje cumpre as normas passar a descumprir, ou seja, não cria `Legado:`.

Na dúvida, proponha.

### Enquanto a proposta aguarda

- Siga a norma ou instrução vigente.
- Se a tarefa não puder ser entregue cumprindo a norma vigente, a proposta é pergunta e a entrega começa com `Preciso de uma decisão.`
- Proposta que o humano não respondeu até a entrega vai para `backlog.md › Propostas`, inteira.

## Proposta

Use este formato na rodada de perguntas ou na entrega:

```markdown
Proposta: <norma nova | alterar <ID> | remover <ID> | mudar <arquivo › seção>>
Motivo: <a lacuna ou o problema, com a evidência>
Texto: <a entrada como ficaria, no modelo de escrita.md>
Impacto: <código que passaria a descumprir, normas e padrões tocados, checagens afetadas>
Alternativas: <cada uma com a consequência, inclusive não mudar nada>
Recomendação: <qual e por quê>
```

Para atrito, proponha a menor mudança que remove a causa. Apagar texto que não orienta decisão conta como correção.

## Registro do implementador

Cada item do campo `Registro` do retorno tem um destino:

- `padrão novo` → `padroes.md`, se cumprir os critérios de `escrita.md › Padrões`.
- `desvio` → justificado: atualize o padrão; sem justificativa: trate como achado com causa `implementação`.
- `armadilha` → `particularidades.md`, se cumprir os critérios de `escrita.md › Particularidades`.
- `lacuna`, `norma ambígua`, `norma conflitante` e `norma que atrapalhou` → avalie o impacto (acima) e aplique ou proponha.

## Registro das mudanças

- Toda mudança aplicada ou proposta é declarada na entrega (`orquestracao.md › 8. Entregue`).
- Mudança motivada por um problema (achado, atrito) também ganha um arquivo em `impactos/`.
- O motivo duradouro de uma norma fica no `Por quê:` dela; quando ela entrou, no `git log`.
