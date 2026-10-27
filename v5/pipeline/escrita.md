# Escrita da pipeline

> Para o orquestrador, ao escrever em `pipeline/`, em `AGENTS.md`, numa ficha ou num brief. Quando e com que autoridade a pipeline muda está em `evolucao.md`.

## Princípio

Clareza não é brevidade. Uma regra clara é estruturada e direta: diz o que fazer, separa o obrigatório da liberdade do agente e explica o porquê quando ele não é óbvio.

- Corte só o que não orienta nenhuma decisão.
- Não encurte uma regra à custa de deixá-la ambígua.
- Uma obrigação por item: uma frase que carrega duas obrigações vira dois itens.
- Exemplo:
  - Verboso: "Quando for criar um componente novo, é importante que você lembre de verificar antes se já existe um componente parecido no projeto e, caso exista, reutilizá-lo em vez de criar outro, para evitar duplicação de código."
  - Estruturado: "Antes de criar um componente, verifique se já existe um equivalente e reutilize-o."

## Vocabulário

- Obrigação: frase imperativa ("Rode", "Cite"). Sem marcador de liberdade, o item é obrigatório.
- Proibição: "Nunca" ou "Não".
- Liberdade: item rotulado `Livre:`, ou frase com "pode" seguida da condição ("Pode rodar em paralelo quando...").
- Exceção: item rotulado `Exceção:`, com o caso exato.
- Motivo: sub-item `Por quê:`, só quando o motivo não é óbvio. Ele diz quando um desvio se justifica.

## Onde mora cada informação

- Registros da pipeline: as fontes de `AGENTS.md › Onde está a verdade`, mais `backlog.md` (o que ficou para depois) e `impactos/` (ocorrências em que a pipeline falhou).
- Como rodar, para pessoas: `README.md`.
- Documentação do produto escrita pelo humano: `docs/`, registrada como fonte em `projeto.md`.
- Estrutura, comportamento e configuração: o próprio código. A pipeline não copia nem aponta o que um agente acha lendo o código; cada linha existe porque, sem ela, um agente competente decidiria pior.
- Decisões de uma tarefa: na entrega e no corpo do commit. As que outras tarefas precisam repetir vão para `padroes.md`.
- Histórico: `git log`. Nenhum arquivo guarda o que já foi feito, exceto `impactos/`, que guarda ocorrências para que a recorrência seja reconhecida.

## Estilo

- Estrutura antes de prosa: `##` por área, `###` por entrada, um fato por item.
- Item rotulado: `- Rótulo: valor`, com os rótulos do modelo do arquivo; sub-itens quando o valor tem partes.
- Cada regra numa fonte só. Em outro arquivo, aponte para ela (`arquivo › título`) em vez de repeti-la ou resumi-la.
- Caminhos, comandos e identificadores entre crases, exatamente como existem e conferidos.
- Só o estado atual: sem datas de progresso, planos ou implementação presumida.
  - Exceção: as datas reais de `backlog.md` e de `impactos/`.
- Tabela só com células curtas; texto longo vai em lista.
  - Por quê: o Prettier alinha as colunas, e uma célula longa alarga todas as linhas.
- Títulos estáveis e únicos: fichas, revisões e outros arquivos citam a entrada pelo título (`padroes.md › <título>`).
- Antes de acrescentar, procure a entrada que já cobre o assunto e edite-a. Entrada que perdeu o objeto sai.

## Normas (`normas.md`)

### Critérios

- Diz o que é obrigatório ou proibido, e por quê.
- É verificável olhando o código.
- Aponta para a fonte da verdade (schema, tema, constantes) em vez de copiar o conteúdo dela.
- Vale para o código do produto e, quando a norma indicar, para arquivos de configuração, respeitando a semântica das ferramentas.
- Se uma funcionalidade comum exige reescrever uma norma, a norma está descrevendo implementação: reescreva-a como limite.
- Exemplos do que cumpre ou viola só entram quando ajudam.
- `Legado:` aponta o código que ainda não cumpre a norma e sai quando não houver mais nenhum.
- Um ID removido não é reaproveitado.
- Normas agrupadas por área (`##`) quando forem várias.

### Modelo

Só os rótulos com conteúdo, nesta ordem. Sem `Checagem:`, a garantia é a revisão; a checagem automática só cabe a norma sem exceção decidida caso a caso.

```markdown
### <ID>: <obrigação ou proibição verificável>

- Por quê: <motivo do limite>
- Escopo: <a que se aplica, quando não é óbvio>
- Como: <detalhe para cumprir>
- Exceção: <caso permitido>
- Checagem: <regra automática que a garante>
- Fonte: <referência existente>
- Legado: <caminho conferido que ainda descumpre a norma>
```

## Padrões (`padroes.md`)

### Critérios

Entra:

- a primeira instância de algo que vai se repetir e em que divergir quebraria a consistência;
- uma decisão que outras tarefas precisam repetir igual;
- qual de duas formas existentes no código é a atual.

Não entra: o que o código já mostra sem ambiguidade, o que uma norma ou uma checagem já garante, uma escolha local, uma intenção ainda não implementada.

### Modelo

Entradas agrupadas por área (`##`):

```markdown
### <nome do padrão>

- Exemplar: `<caminho existente e conferido>`
- Como: <forma ou decisão a repetir; sub-itens quando houver várias>
- Por quê: <o que quebra sem ela>
```

## Projeto (`projeto.md`)

- Só fatos conferidos no destino: não registre como existente, instalado, disponível, confiável ou testado o que não foi conferido.
- Aponte para as fontes reais; não copie o conteúdo delas nem registre uma implementação presumida.
- Estado de adoção: o atual, sem histórico.
- Fontes de referência: só as que ficam fora do código ou que uma norma manda registrar, numa `### <área>` por assunto, com itens `` - <papel>: `<caminho>` ``.

## Particularidades (`particularidades.md`)

### Critérios

Entra:

- a armadilha que faria um agente competente errar ou perder tempo;
- a limitação conhecida que pesa numa decisão;
- a decisão cujo motivo o código não mostra.

Não entra: o que o código, a configuração ou a documentação oficial já dizem, a forma a repetir (padrão), a obrigação ou proibição (norma), a operação para pessoas (`README.md`).

### Modelo

Só os rótulos que se aplicam, agrupados por área:

```markdown
## <área>

- Atenção: <armadilha e o que fazer>
- Limitação: <limite e quando ele importa>
- Decisão: <escolha>
  - Por quê: <motivo>
```

## Backlog (`backlog.md`)

### Critérios

Entra:

- achado confirmado fora do escopo da tarefa;
- achado não crítico que ficou aberto depois do último ciclo de revisão;
- proposta de mudança na pipeline que aguarda aprovação;
- pendência que o humano adiou.

Não entra: defeito do trabalho entregue (corrija antes), achado sem base, funcionalidade que ninguém pediu, assunto que já tem entrada.

- Uma entrada sai quando é resolvida, quando o humano a recusa ou quando perde o objeto.
- Entradas agrupadas em `## Achados`, `## Propostas` e `## Pendências`.

### Modelo

Só os rótulos que se aplicam:

```markdown
### <título curto e único>

- Gravidade: crítico | desvio
- Onde: `<caminho:linha>` ou <área>
- O quê: <o problema, a pendência ou o texto da proposta>
- Evidência: <reprodução, trecho ou referência>
- Origem: <AAAA-MM-DD real>, <o pedido em poucas palavras>
- Recomendação: <o que fazer e por quê>
```

- `Gravidade` só em achados, com os valores de `revisao.md › Gravidade`.
- Numa proposta, `O quê` traz a proposta inteira no formato de `evolucao.md › Proposta`, para que ela possa ser aprovada depois sem ser refeita.

## Impactos (`impactos/`)

- Ocorrências reais desta instalação em que uma instrução da pipeline causou ou não evitou um problema: achado com causa `pipeline` ou `indeterminada`, retrabalho, pergunta desnecessária, resíduo ou reclamação do humano.
- Arquivo: `impactos/<AAAA-MM-DD>-<assunto>.md`, com a data real.
- Sem incidentes hipotéticos.

```markdown
# <AAAA-MM-DD>: <o que aconteceu>

Causa: pipeline (<norma ou instrução> ausente | ambígua | contraditória | desatualizada) | indeterminada (<hipóteses>)

Efeito: <o que se observou>

Correção: <o que mudou no código e na pipeline; mudança só proposta fica como "proposta, aguarda aprovação">
```
