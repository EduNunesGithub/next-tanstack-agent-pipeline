# Escrita

> Para: orquestrador · Leia quando: ao escrever em `pipeline/` ou em `AGENTS.md`.

Quando e com que autoridade a pipeline muda está em `guias/evolucao.md`. Este guia diz como escrever.

## Princípio

Clareza não é brevidade. Uma instrução clara é estruturada e direta: diz o que fazer, separa o obrigatório da liberdade e explica o porquê quando ele não é óbvio.

- Corte só o que não orienta nenhuma decisão.
- Não encurte uma instrução à custa de deixá-la ambígua.
- Uma obrigação por item: frase que carrega duas obrigações vira dois itens.
- Exemplo:
  - Prolixo: "Sempre que for necessário exibir um valor monetário, é importante lembrar de usar a função de formatação que já existe no projeto, para que todos os valores apareçam do mesmo jeito em todas as telas."
  - Estruturado: "Valor monetário exibido usa o formatador do projeto."

## Vocabulário

- Obrigação: frase imperativa ("Rode", "Cite"). Item sem marcador de liberdade é obrigatório.
- Proibição: "Nunca" ou "Não".
- Liberdade: item rotulado `Livre:`, ou frase com "pode" seguida da condição ("Pode rodar enquanto…").
- Exceção: item rotulado `Exceção:`, com o caso exato.
- Motivo: sub-item `Por quê:`, só quando o motivo não é óbvio. Ele diz quando um desvio se justifica.

## Onde mora cada coisa

- Fontes, regras, padrões e armadilhas: na área do assunto, em `conhecimento/`, achada pelo índice.
- Fatos do projeto que o código não mostra: `projeto.md`.
- O que ficou para depois: `backlog.md`. Vezes em que a pipeline falhou: `ocorrencias/`.
- Processo: `papeis/` e `guias/`. O que vale para todos os agentes: `AGENTS.md`.
- Como rodar, para pessoas: o `README.md` da aplicação. Uso da pipeline, para pessoas: `pipeline/README.md`.
- Documentação do produto escrita pelo humano: `docs/`, registrada nas `Fontes` da área do assunto.
- Estrutura, comportamento e configuração: o próprio código. A pipeline não copia nem aponta o que um agente acha lendo o código; cada linha existe porque, sem ela, um agente competente decidiria pior.
- Decisões de uma tarefa: a entrega e o commit (`papeis/orquestrador.md › Decisões tomadas sem perguntar`).
- Histórico: o `git log`. Só `ocorrencias/` guarda o passado, para que a recorrência seja reconhecida.

## Estilo

- Todo documento da pipeline abre com `# Título` e, logo abaixo, `> Para: <papéis> · Leia quando: <gatilho>`.
  - Documento novo lido por agente entra em `AGENTS.md › Mapa` com o mesmo texto do cabeçalho; área nova entra em `conhecimento/indice.md`, com o gatilho igual ao `Leia quando`.
- Estrutura antes de prosa: `##` por assunto, `###` por entrada, um fato por item.
- Item rotulado: `- Rótulo: valor`, com os rótulos do modelo; sub-itens quando o valor tem partes.
- Cada regra numa fonte só. Em outro lugar, aponte para ela em vez de repeti-la ou resumi-la.
- Referência a um título: o caminho e o título, separados por `›`, tudo numa única crase, com o caminho relativo a `pipeline/`, ou à raiz para os arquivos da raiz. Ex.: `guias/evolucao.md › Proposta`.
- Caminhos, comandos e identificadores entre crases, exatamente como existem e conferidos.
- Só o estado atual: sem datas de progresso, planos ou implementação presumida.
  - Exceção: as datas reais de `backlog.md` e de `ocorrencias/`.
- Tabela só com células curtas; texto longo vai em lista.
  - Por quê: o Prettier alinha as colunas, e uma célula longa alarga todas as linhas.
- Títulos estáveis e únicos dentro do arquivo: missões, briefs e outros documentos os citam.
- Antes de acrescentar, procure a entrada que já cobre o assunto e edite-a. Entrada que perdeu o objeto sai.
- Antes de entregar, faça a `Conferência`.

## Conferência

Antes de entregar uma mudança em `pipeline/`, `AGENTS.md`, `.claude/` ou `.codex/`, confira:

- cada referência `arquivo › título` aponta para um título que existe;
- cada caminho em crase existe, inclusive os de `Exemplar:`, `Legado:`, `Anterior:` e das `Fontes`;
- o `Mapa` de `AGENTS.md` repete, igual, o cabeçalho de cada documento, e todo documento lido por agente está nele;
- o índice lista toda área, com o gatilho igual ao `Leia quando` dela, e cada ID de regra é único e usa o prefixo da área;
- `projeto.md › Arquivos protegidos` e as regras `ask` de `.claude/settings.json` se correspondem, e cada regra de git existe para Bash e para PowerShell;
- `.claude/agents/` e `.codex/agents/` têm os mesmos agentes, com a mesma descrição e as mesmas instruções;
- os títulos são únicos dentro de cada arquivo;
- o formato passa (`projeto.md › Checagens`).

## Regra

Critérios:

- Diz o que é obrigatório ou proibido, e por quê.
- É verificável olhando o código.
- Aponta a fonte da verdade (schema, tema, constantes) em vez de copiar o conteúdo dela.
- Vale para o código do produto e, quando a regra diz, para arquivos de configuração, respeitando a semântica das ferramentas.
- Se uma funcionalidade comum obriga a reescrever a regra, ela está descrevendo implementação: reescreva-a como limite.
- Exemplo do que cumpre ou viola só entra quando ajuda.
- O ID usa o prefixo da área e o próximo número livre. ID removido não volta a ser usado.
- `Legado:` lista o código conhecido que ainda descumpre a regra e sai quando não sobra nenhum.

Modelo, só com os rótulos que têm conteúdo e nesta ordem. Sem `Checagem:`, quem garante a regra é a revisão; checagem automática só cabe a regra sem exceção decidida caso a caso:

```markdown
### <ID>: <obrigação ou proibição verificável>

- Por quê: <motivo do limite>
- Escopo: <a que se aplica, quando não é óbvio>
- Como: <detalhe para cumprir>
- Exceção: <caso permitido>
- Checagem: <regra automática que a garante>
- Fonte: <referência existente, em Fontes>
- Legado: `<caminho conferido que ainda descumpre a regra>`
```

## Padrão

Entra:

- a primeira instância de algo que vai se repetir e em que divergir quebraria a consistência;
- uma decisão que outras tarefas precisam repetir igual;
- qual de duas formas que convivem no código é a atual.

Não entra: o que o código já mostra sem ambiguidade, o que uma regra ou uma checagem já garante, uma escolha local, uma intenção ainda não implementada.

Modelo:

```markdown
### <nome do padrão>

- Exemplar: `<caminho existente e conferido>`
- Como: <a forma ou a decisão a repetir; sub-itens quando houver várias>
- Por quê: <o que quebra sem ela>
- Anterior: `<caminho na forma antiga, que não se imita>`
```

## Armadilha

Entra:

- a armadilha que faria um agente competente errar ou perder tempo;
- a limitação conhecida que pesa numa decisão;
- a decisão cujo motivo o código não mostra.

Não entra: o que o código, a configuração ou a documentação oficial já dizem, a forma a repetir (padrão), a obrigação ou proibição (regra), a operação para pessoas (`README.md`).

Modelo, só com os rótulos que se aplicam:

```markdown
### <título curto>

- Atenção: <a armadilha e o que fazer>
- Limitação: <o limite e quando ele importa>
- Decisão: <a escolha>
  - Por quê: <o motivo>
```

## Fonte

- Entra só o que fica fora do código lido de passagem ou o que uma regra manda registrar.
- Item na seção `Fontes` da área: `` - <papel>: `<caminho>` ``.

## Projeto

- Só fatos conferidos no destino: nada registrado como existente, instalado, disponível, confiável ou testado sem conferência.
- Aponte as fontes reais; não copie o conteúdo delas nem registre implementação presumida.
- Adoção: o estado atual, sem histórico.

## Backlog

Entra:

- achado confirmado fora do escopo da tarefa;
- achado de consistência que sobrou do último ciclo de revisão;
- proposta de mudança na pipeline que aguarda aprovação;
- pendência que o humano adiou ou que uma entrega parcial deixou.

Não entra: defeito do trabalho entregue (corrija antes), achado sem base, funcionalidade que ninguém pediu, assunto que já tem entrada.

- Uma entrada sai quando é resolvida, quando o humano a recusa ou quando perde o objeto.
- Entradas agrupadas em `Achados`, `Propostas` e `Pendências`.

Modelo, só com os rótulos que se aplicam:

```markdown
### <título curto e único>

- Classe: crítico | consistência
- Onde: `<caminho:linha>` ou <área>
- O quê: <o problema, a pendência ou a proposta>
- Evidência: <reprodução, trecho ou referência>
- Origem: <AAAA-MM-DD real>, <o pedido em poucas palavras>
- Recomendação: <o que fazer e por quê>
```

- `Classe` só em achados: a do revisor, ou a que você deu ao reclassificar.
- Numa proposta, `O quê` traz a proposta inteira no formato de `guias/evolucao.md › Proposta`, para que ela possa ser aprovada depois sem ser refeita.
- Numa pendência de entrega parcial, `O quê` diz o que falta e onde o trabalho parou, para outra sessão retomar.

## Ocorrência

- Só ocorrências reais desta instalação em que uma instrução da pipeline causou ou não evitou um problema: achado ou falha de causa `pipeline` ou `indeterminada`, retrabalho, pergunta desnecessária, resíduo, reclamação do humano.
- Um arquivo por ocorrência, em `ocorrencias/`, com o nome `<AAAA-MM-DD>-<assunto>.md` e a data real.
- Sem incidentes hipotéticos.

```markdown
# <AAAA-MM-DD>: <o que aconteceu>

Causa: pipeline (<regra ou instrução> ausente | ambígua | contraditória | desatualizada) | indeterminada (<hipóteses>)

Efeito: <o que se observou>

Correção: <o que mudou no código e na pipeline; mudança só proposta fica como "proposta, aguarda aprovação">
```
