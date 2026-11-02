# Evolução

> Para: orquestrador · Leia quando: um gatilho de mudança na pipeline dispara.

Este guia diz quando a pipeline muda e com que autoridade. Como escrever cada entrada está em `guias/escrita.md`.

## Gatilhos

1. **Cobertura:** o pedido leva o projeto a terreno sem regra nem padrão (`papeis/orquestrador.md › Cobertura`).
2. **Causa `pipeline`:** de uma falha ou de um achado (`guias/falhas.md › Causa`).
3. **Sinal do relato:** `lacuna`, `conflito` ou `atrito`, e o `legado` ou a escolha entre duas formas que pedem registro (`papeis/orquestrador.md › Sinais do relato`).
4. **Instrução duradoura do humano:** "a partir de agora, sempre X". Se não está claro que ela é duradoura, vale só para a tarefa atual.
5. **Mudança de convenção:** o humano aprova trocar uma forma estabelecida por outra.
6. **Atrito:** uma instrução causou retrabalho, pergunta desnecessária ou resíduo, ou o humano reclamou de um comportamento.

## Avalie o impacto

Antes de escrever, responda:

- Sem a entrada, agentes competentes decidiriam de formas diferentes ou erradas? Se não, não escreva nada.
- Qual é o tipo certo: regra, padrão, armadilha, fonte, fato de projeto ou item de backlog? Os critérios de cada um estão em `guias/escrita.md`.
- Em que área? Na que o gatilho de leitura levaria quem precisa da entrada. Se nenhuma serve, área nova (`Áreas`).
- Que código existente passaria a descumprir a entrada? Que regras, padrões e decisões ela toca?
- Quais são as alternativas, inclusive não escrever nada, e a consequência de cada uma?

Uma biblioteca nova costuma pedir duas entradas, em momentos diferentes:

- uma regra antes de delegar, quando resta uma escolha que a tabela de `conhecimento/stack.md` e as regras não fecham (por exemplo, com que campos se compõe um formulário);
- um padrão depois da primeira instância, que registra a forma de uso com o exemplar.

Se as regras e a tabela já fecham a escolha, a cobertura termina sem escrever nada, e esse é um resultado válido.

## Aplique ou proponha

### Aplique e declare

- Regra nova, aditiva e sem conflito.
- Padrão ou armadilha novo, alterado ou removido, inclusive o `Anterior:` de um padrão.
  - Por quê: padrões e armadilhas registram formas e cuidados, não limites; o padrão já admite desvio justificado e atualização.
- Fonte de referência conferida, nas `Fontes` de uma área.
- Área nova com conteúdo aditivo: o arquivo e a entrada dele em `conhecimento/indice.md`.
- Manutenção de uma regra que não muda o que ela exige:
  - acrescentar o `Checagem:` que a garante;
  - acrescentar ao `Legado:` um código que já a descumpria;
  - tirar do `Legado:` um caminho que passou a cumprir;
  - atualizar um caminho que mudou de lugar.
- Fato conferido em `projeto.md`: adoção, checagens, como rodar, paralelismo, ambiente, arquivo protegido novo com a regra `ask` correspondente em `.claude/settings.json`.
- Entradas de `backlog.md` e de `ocorrencias/`.

### Proponha e aguarde

- Alterar ou remover uma regra.
- Regra nova com conflito.
- Qualquer mudança em `AGENTS.md`, `CLAUDE.md`, `papeis/` e `guias/`.
- Mudar o gatilho ou o prefixo de uma área em `conhecimento/indice.md`, inclusive ao dividi-la.
- Mudar a tabela ou as regras de `conhecimento/stack.md`.
- Mudar `projeto.md › Idioma`.
- Mudar as definições de agente ou as configurações de `.claude/` e `.codex/`, salvo a regra `ask` de um arquivo protegido novo.
- Tirar um arquivo de `projeto.md › Arquivos protegidos`.
- Por quê: essas mudanças valem para todas as tarefas seguintes, e um erro nelas se repete em cada uma.

Exceção: um pedido explícito do humano para mudar uma regra ou instrução ("troque UI-7 por…", "a partir de agora, sempre X") já é a aprovação. Aplique e declare.

- Conflito entre o pedido e uma regra que o humano não mencionou não é aprovação: é pergunta (`papeis/orquestrador.md › Autonomia`).

### Aditiva e sem conflito

Uma entrada nova é aditiva e sem conflito quando todas estas condições valem:

- não contradiz, não restringe e não amplia uma regra, um padrão ou uma decisão registrada;
- não escolhe entre duas formas que já convivem no código;
- não cria `Legado:`: nenhum código que hoje cumpre as regras passa a descumpri-las.

Na dúvida, proponha.

### Enquanto a proposta aguarda

- Siga a regra ou a instrução vigente.
- Se a tarefa não pode ser entregue cumprindo a vigente, a proposta é pergunta, e a entrega começa com `Preciso de uma decisão.`
- Na entrega, toda proposta ainda sem resposta vai inteira para `backlog.md`, em `Propostas`. Sai de lá quando o humano aprovar ou recusar.

## Proposta

Use este formato na rodada de perguntas ou na entrega:

```markdown
Proposta: <regra nova | alterar <ID> | remover <ID> | mudar <arquivo › seção>>
Motivo: <a lacuna ou o problema, com a evidência>
Texto: <a entrada como ficaria, no modelo de guias/escrita.md>
Impacto: <código que passaria a descumprir, regras e padrões tocados, checagens afetadas>
Alternativas: <cada uma com a consequência, inclusive não mudar nada>
Recomendação: <qual e por quê>
```

Para atrito, proponha a menor mudança que remove a causa. Apagar texto que não orienta nenhuma decisão conta como correção.

## Deriva

O código antigo só deixa de ser imitado quando a pipeline diz onde ele está.

### Legado sinalizado

- O sinal `legado`, ou uma linha de `Fora do escopo:` do revisor, aponta código fora de uma regra que o `Legado:` dela não lista.
- Confira o trecho e acrescente o caminho ao `Legado:`. É manutenção: aplique e declare.

### Duas formas

Quando duas formas de fazer a mesma coisa convivem no código:

- Se uma delas descumpre uma regra, a atual é a outra; a que descumpre é legado.
- Se as duas cumprem, a atual é a que o implementador acabou de usar, salvo motivo concreto para a outra, como ser a mais difundida no projeto ou a que a documentação da biblioteca recomenda.
- Registre a escolha como padrão: `Exemplar:` na forma atual, `Anterior:` na outra, e o motivo em `Por quê:`. Declare na entrega.
- Registrar a forma atual como padrão é aplicar e declarar. Transformá-la em regra escolhe entre formas que convivem, e por isso é proposta.
- Se a escolha muda o produto, é pergunta.

### Mudança de convenção

Quando o humano aprova trocar uma forma estabelecida por outra, a entrega da mudança inclui:

1. A regra ou o padrão atualizado.
2. O inventário do código que passa a descumprir a regra: uma missão de exploração `t0` localiza e lista, e os caminhos vão para o `Legado:`.
3. Os padrões e os exemplares ajustados:
   - o exemplar na forma antiga passa para `Anterior:`;
   - o padrão ganha um `Exemplar:` na forma nova; enquanto não houver um, fica só com `Como:` e `Anterior:`, e a próxima missão que criar a forma nova é avisada no `Contexto` de que é a primeira instância.
4. A migração do código antigo, que é opcional: um item em `backlog.md`, em `Pendências`, a menos que o pedido já a cubra.

## Áreas

- Crie uma área quando um assunto ganha regras ou padrões que nenhum gatilho existente levaria a ler. A área nova tem:
  - o arquivo, com o cabeçalho e as seções `Fontes`, `Regras`, `Padrões` e `Armadilhas`;
  - a entrada em `conhecimento/indice.md`, com arquivo, prefixo e um gatilho mecânico (extensão, pasta, tipo de arquivo, dependência).
- Quando uma área pesa em missões que só usam parte dela, proponha dividi-la. Cada parte ganha o seu gatilho; as regras mantêm o ID, e as áreas resultantes podem compartilhar o prefixo.
- Depois de qualquer mudança nas áreas, faça a conferência de `guias/escrita.md › Conferência`.

## Registro

- Toda mudança aplicada ou proposta é declarada na entrega (`papeis/orquestrador.md › 7. Entregue`).
- Mudança motivada por um problema (causa `pipeline` ou `indeterminada`, retrabalho, pergunta desnecessária, resíduo, reclamação) também ganha uma ocorrência (`guias/escrita.md › Ocorrência`).
- O motivo duradouro de uma regra fica no `Por quê:` dela; quando ela entrou, no `git log`.
