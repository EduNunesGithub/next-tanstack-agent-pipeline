# Reparo

A pipeline muda quando causa ou não evita um problema, na mesma tarefa, sem pedir licença. As exceções estão em `Só com o humano`. Tarefa sem gatilho não escreve em `ia/`.

## Gatilhos

Do humano:

- corrigiu um comportamento: "não faça assim", "isso está errado";
- deu instrução duradoura: "a partir de agora", "sempre", "nunca". Sem sinal de que dura, vale só para a tarefa;
- repetiu uma instrução que já tinha dado.

Seus:

- falha ou achado de causa `pipeline` (`ia/quando/falha.md`);
- aviso de executor ou `Pipeline:` do auditor, confirmado no código;
- problema que uma linha de `ia/` já cobria e voltou a acontecer;
- escolha de terreno novo que é obrigação e o código pronto não mostraria (`ia/fluxo.md › Terreno novo`);
- referência quebrada, instrução contraditória ou sem objeto, vista de passagem.

Não é gatilho: erro isolado que a checagem ou a conferência pegou; primeira ocorrência de uma forma; tarefa que correu bem.

## Passos

1. **Efeito.** Corrija o problema da tarefa pelo caminho normal.
2. **Causa.** Ache a linha que deixou acontecer: `ausente`, `ambígua`, `contraditória`, `velha`, `não lida` (nenhum gatilho levou até ela) ou `ignorada` (lida e não seguida).
3. **Remédio.** O primeiro desta lista que remove a causa:
   1. **Nada.** Um agente competente, com o código e as regras de hoje, acertaria. Vale para a `ignorada` que uma checagem ou a conferência pega.
   2. **Menos texto.** `ambígua`: reescreva a linha, sem acrescentar outra. `contraditória`: fique com uma. `velha`: atualize ou apague.
   3. **Checagem ou código.** Uma ferramenta verifica o erro sem exceção caso a caso (lint, tipo, teste), ou o código pode torná-lo impossível: encomende. A mensagem da checagem diz o que fazer; a regra, se existir, ganha `Garantia:`.
   4. **Posição.** `não lida`, ou `ignorada` que nada pega: leve a linha para o momento da ação (o modelo da encomenda, `ia/executor.md › Antes de retornar` ou `ia/fluxo.md › 4. Confira`), ou corrija o gatilho. Nunca uma segunda linha.
   5. **Texto.** Só para `ausente`, e só o que passa em `Entra em ia/`.
   6. **Humano.** A linha já está no momento da ação e o problema voltou: leve o diagnóstico e as opções.
4. **Prova.** Releia como um agente novo, que carrega só o que os gatilhos mandam. Ele acertaria agora? Se não, volte ao 3.
5. **Declare** o reparo na entrega, numa linha.

## Entra em `ia/`

Uma entrada nova responde sim às três perguntas:

1. Um agente que lê o código, a árvore de pastas, a configuração e a documentação oficial erraria sem ela?
2. Nenhuma checagem recusa o erro, nem pode recusar a custo razoável?
3. Nenhuma linha existente cobre o assunto? Se cobre, edite-a.

Nunca entra (`AGENTS.md › Leis`, 5):

- onde algo fica, como se chama, o que recebe, como foi feito, o que existe. Não há catálogo: a árvore de pastas lista as unidades pelo nome (`ia/regras/codigo.md › C11`);
- a forma de um tipo de arquivo: o exemplar é código, e a encomenda o aponta;
- histórico, que é do `git log`; intenção ainda não implementada, que é do plano do projeto.

Teto: assunto com mais de 150 linhas não recebe entrada antes de enxugar (sai o que virou checagem ou o que o código passou a mostrar) ou de se dividir (`Assunto novo`).

### Onde mora

| O que é                                             | Lugar                               |
| --------------------------------------------------- | ----------------------------------- |
| Obrigação ou proibição verificável no código        | regra, em `ia/regras/<assunto>.md`  |
| Armadilha que o código não mostra                   | alerta, no assunto                  |
| Código que descumpre uma regra                      | `Dívida:` da regra                  |
| Como instalar, rodar e checar                       | `README.md` da aplicação            |
| O que só agente usa para operar e o README não traz | `ia/fatos.md`                       |
| O que fica para depois e ninguém acharia            | `ia/pendencias.md`                  |
| Processo de um papel                                | o arquivo do papel, ou `ia/quando/` |
| O que vale para todo agente                         | `AGENTS.md`                         |

### Regra

Só com os rótulos que têm conteúdo, nesta ordem. O ID usa o prefixo do assunto e o próximo número; ID removido não volta.

```markdown
### <ID> · <nome curto>

<A obrigação ou proibição, verificável olhando o código.>

- Porque: <o motivo do limite>
- Vale para: <o alcance, quando não é óbvio>
- Como: <detalhe para cumprir>
- Exceto: <o caso permitido>
- Garantia: <a checagem automática que a verifica>
- Fonte: `<o arquivo que é a verdade, quando não se acha pelo nome>`
- Dívida: `<caminho conferido que ainda descumpre>`
```

- Sem `Garantia:`, quem garante é a auditoria.
- A regra aponta, nunca descreve: `Fonte:` é um caminho, sem resumo do que há nele.
- Se uma funcionalidade comum obriga a reescrever a regra, ela descreve implementação: reescreva-a como limite.

### Alerta

```markdown
### <título curto>

- Cuidado: <a armadilha, o que fazer e o caminho a que ela se refere>
- Porque: <o motivo que o código não mostra>
```

- Entra: o que já custou um erro e voltaria a custar.
- Sai: quando o código muda e a armadilha deixa de existir. Quem altera o caminho citado confere.

### Duas formas

Duas formas de fazer a mesma coisa convivem no código, ou o humano trocou uma forma por outra:

- Uma descumpre uma regra: é dívida; a atual é a outra.
- As duas cumprem: a atual é a que o humano pediu ou a que acabou de ser usada, salvo motivo concreto para a outra. Registre uma regra de uma linha, com `Fonte:` na atual e `Dívida:` na outra.
- A escolha muda o produto: é pergunta.
- Migrar o código antigo é pendência, salvo se o pedido cobre.

### Assunto novo

- Crie quando regras novas não seriam lidas por nenhum gatilho existente, ou quando um assunto passa do teto: o arquivo em `ia/regras/`, com `Regras` e, se houver, `Alertas`, e a linha na tabela de `AGENTS.md`.
- Gatilho mecânico: extensão, pasta, tipo de arquivo, dependência.
- Na divisão, as regras mantêm o ID.

## Só com o humano

Aplique sozinho tudo, menos:

- mudar o que uma regra exige, ou removê-la. Esclarecer a redação sem mudar a exigência não conta;
- regra nova que transforma em dívida código que hoje cumpre, ou que escolhe entre duas formas vivas;
- a tabela de `ia/regras/bibliotecas.md`;
- as `Leis` de `AGENTS.md`;
- modelo, esforço, ferramentas e permissões em `.claude/` e `.codex/`. Exceto: a regra `Edit(…)` de um protegido novo.

Porque: são decisões do humano, e um erro nelas se repete em toda tarefa.

- Pedido explícito do humano já é a aprovação: aplique.
- Sem pedido: siga a instrução vigente e leve a proposta na entrega: a mudança, o motivo com a evidência, o texto novo, o que vira dívida e as alternativas. Guarde-a em `ia/pendencias.md` até a resposta.
- A tarefa não fecha cumprindo a vigente: é pergunta, agora.

## Como escrever

- Curto e direto, sem admitir duas leituras. Uma obrigação por item.
- Obrigação no imperativo. Proibição com `Nunca` ou `Não`. Exceção em `Exceto:`. Motivo em `Porque:`, só quando não é óbvio.
- Cada coisa num lugar só. Nos outros, aponte: `arquivo › título`.
- Edite a linha que já cobre o assunto antes de criar outra. Apague o que perdeu o objeto. Seção vazia não se escreve.
- Só o estado atual: sem datas, planos ou histórico.
- Caminhos, comandos e identificadores entre crases, conferidos. Tabela só com células curtas.
- Títulos estáveis. Mudou um título, um caminho, um ID ou o nome de um agente: busque as citações no repositório e atualize todas.
- `.claude/agents/` e `.codex/agents/` têm os mesmos agentes: mudou numa pasta, mude na outra.
- Formato: `ia/fatos.md › Checagens`.
