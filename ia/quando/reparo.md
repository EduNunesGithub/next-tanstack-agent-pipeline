# Reparo

Quando a pipeline causa ou não evita um problema, ela muda na mesma tarefa, sem pedir licença. As exceções estão em `Só com o humano`.

## Gatilhos

Do humano:

- corrigiu um comportamento: "não faça assim", "isso está errado";
- deu instrução duradoura: "a partir de agora", "sempre", "nunca". Sem sinal de que dura, vale só para a tarefa;
- repetiu uma instrução que já tinha dado.

Seus:

- falha ou achado de causa `pipeline` (`ia/quando/falha.md`);
- aviso de executor, ou `Pipeline:` e `De passagem:` do auditor;
- retrabalho, pergunta que o humano não precisava responder, resíduo deixado no repositório;
- terreno novo com escolha aberta (`ia/fluxo.md › Terreno novo`);
- referência quebrada, instrução contraditória ou sem objeto, vista de passagem.

## Passos

1. **Efeito.** Corrija o problema da tarefa pelo caminho normal.
2. **Causa.** Ache a linha que deixou acontecer e classifique:
   - `ausente`: nenhuma instrução cobria;
   - `ambígua`: admitia a leitura errada;
   - `contraditória`: duas instruções divergiam;
   - `velha`: descrevia algo que mudou;
   - `não lida`: existia, mas nenhum gatilho levou até ela;
   - `ignorada`: foi lida e não foi seguida.
3. **Recorrência.** Procure o sintoma em `ia/diario.md`. Já está lá: `Escada`.
4. **Remédio.** A menor mudança que remove a causa:
   - `ausente`: entrada nova, no tipo e no lugar de `Onde mora`;
   - `ambígua`: reescreva a linha; não acrescente outra;
   - `contraditória`: fique com uma e apague a outra;
   - `velha`: atualize ou apague;
   - `não lida`: corrija o gatilho, ou leve a linha para onde ela é lida;
   - `ignorada`: nada muda; só o registro.
5. **Prova.** Releia como um agente novo, que carrega só o que os gatilhos mandam. Ele acertaria agora? Se não, volte ao 4.
6. **Registro.** Uma linha em `ia/diario.md`, e o reparo declarado na entrega.

Não mudar nada é resultado válido: se um agente competente já decidiria certo, não escreva.

## Escada

Sintoma repetido prova que o remédio anterior não funcionou. Suba um degrau; não repita o mesmo tipo de remédio.

1. **Texto:** o passo 4.
2. **Posição:** leve a instrução para o momento da ação: o modelo da encomenda, `ia/executor.md › Antes de retornar` ou `ia/fluxo.md › 4. Confira`.
3. **Ferramenta:** regra verificável sem exceção caso a caso vira checagem do produto (lint, tipo, teste), citada no `Garantia:` da regra.
4. **Humano:** terceiro registro do mesmo sintoma. Leve o diagnóstico e as opções.

## Só com o humano

Aplique sozinho tudo, menos:

- mudar o que uma regra exige, ou removê-la. Esclarecer a redação sem mudar a exigência não conta;
- regra nova que transforma em dívida código que hoje cumpre, ou que escolhe entre duas formas vivas;
- a tabela de `ia/regras/bibliotecas.md`;
- as `Leis` de `AGENTS.md`;
- modelo, esforço, ferramentas e permissões em `.claude/` e `.codex/`. Exceto: a regra `Edit(…)` de um protegido novo.

Porque: são decisões do humano, e um erro nelas se repete em toda tarefa.

Nesses casos:

- Pedido explícito do humano já é a aprovação: aplique.
- Sem pedido: siga a instrução vigente e leve a proposta pronta na entrega. Guarde-a em `ia/pendencias.md` até a resposta.
- A tarefa não fecha cumprindo a vigente: é pergunta, agora.

```markdown
Proposta: <a mudança>
Motivo: <o problema, com a evidência>
Texto: <como a entrada ficaria>
Impacto: <o que vira dívida, o que mais é tocado>
Alternativas: <cada uma com a consequência, inclusive não mudar>
```

## Onde mora

| O que é                                      | Lugar                               |
| -------------------------------------------- | ----------------------------------- |
| Obrigação ou proibição verificável no código | regra, em `ia/regras/<assunto>.md`  |
| Forma a repetir igual                        | molde, no assunto                   |
| O que o código não mostra e faria errar      | alerta, no assunto                  |
| Código que descumpre uma regra               | `Dívida:` da regra                  |
| Comando, porta, recurso, estado do projeto   | `ia/fatos.md`                       |
| O que fica para depois                       | `ia/pendencias.md`                  |
| Processo de um papel                         | o arquivo do papel, ou `ia/quando/` |
| O que vale para todo agente                  | `AGENTS.md`                         |
| Como rodar, para pessoas                     | `README.md` da aplicação            |

Não mora em lugar nenhum: o que um agente acha lendo o código; histórico, que é do `git log`; intenção ainda não implementada.

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
- Fonte: `<o arquivo que é a verdade; a regra aponta, não copia>`
- Dívida: `<caminho conferido que ainda descumpre>`
```

- Sem `Garantia:`, quem garante é a auditoria.
- Se uma funcionalidade comum obriga a reescrever a regra, ela descreve implementação: reescreva-a como limite.

### Molde

```markdown
### <nome>

- Exemplar: `<caminho conferido>`
- Como: <a forma ou a decisão a repetir>
- Porque: <o que quebra sem ela>
- Antes: `<caminho na forma antiga, que não se imita>`
```

- Entra: primeira instância de algo que vai se repetir; decisão que outras tarefas precisam repetir igual; qual de duas formas vivas é a atual.
- Não entra: o que o código mostra sem ambiguidade, o que uma regra ou checagem já garante, escolha local.

### Alerta

```markdown
### <título curto>

- Cuidado: <a armadilha ou o limite, e o que fazer>
- Porque: <o motivo que o código não mostra>
```

- Não entra: o que o código, a configuração ou a documentação oficial já dizem.

### Duas formas

Duas formas de fazer a mesma coisa convivem no código:

- Uma descumpre uma regra: é dívida; a atual é a outra.
- As duas cumprem: a atual é a que acabou de ser usada, salvo motivo concreto para a outra (mais difundida, recomendada pela documentação).
- Registre o molde, com `Exemplar:` na atual e `Antes:` na outra.
- A escolha muda o produto: é pergunta.

### Convenção trocada

O humano trocou uma forma estabelecida por outra:

1. Atualize a regra ou o molde.
2. Uma exploração `executor-1` lista o código que passou a descumprir: vai para o `Dívida:`.
3. O exemplar antigo passa para `Antes:`. Sem exemplar novo ainda, a próxima encomenda é avisada de que cria a primeira instância.
4. A migração do código antigo é pendência, salvo se o pedido a cobre.

### Assunto novo

- Crie quando regras ou moldes novos não seriam lidos por nenhum gatilho existente: o arquivo em `ia/regras/`, com `Regras`, `Moldes` e `Alertas`, e a linha na tabela de `AGENTS.md`.
- Gatilho mecânico: extensão, pasta, tipo de arquivo, dependência.
- Assunto que pesa em encomendas que usam só parte dele: divida. As regras mantêm o ID.

## Como escrever

- Curto e direto. Se uma frase de poucas palavras dá o contexto, não use um parágrafo.
- Nunca encurte a ponto de admitir duas leituras.
- Uma obrigação por item.
- Obrigação no imperativo. Proibição com `Nunca` ou `Não`. Exceção em `Exceto:`. Motivo em `Porque:`, só quando não é óbvio.
- Cada coisa num lugar só. Nos outros, aponte: `arquivo › título`.
- Edite a linha que já cobre o assunto antes de criar outra. Apague o que perdeu o objeto.
- Só o estado atual: sem datas, planos ou histórico.
  - Exceto: `ia/diario.md` e `ia/pendencias.md`.
- Caminhos, comandos e identificadores entre crases, conferidos.
- Tabela só com células curtas.
- Títulos estáveis: outros arquivos os citam.
- Mudou um título, um caminho, um ID ou o nome de um agente: busque as citações no repositório e atualize todas.
- `.claude/agents/` e `.codex/agents/` têm os mesmos agentes: mudou numa pasta, mude na outra.
- Formato: `ia/fatos.md › Checagens`.
