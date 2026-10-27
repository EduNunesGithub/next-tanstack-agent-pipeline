# Changelog

> Evolução do template da pipeline. Não vai para o destino (`pipeline/adocao.md`).

## v5

### Resumo

A v5 mantém o núcleo da v4: normas com motivo, fichas com arquivos fechados, cinco níveis de implementador, ondas paralelas com arquivos disjuntos, conferência pelo diff e revisor independente. O que muda:

- o orquestrador pergunta menos e registra o que decidiu sozinho;
- os achados de revisão têm gravidade, escopo e causa, com limite de ciclos e backlog;
- a pipeline evolui de forma proativa, com regra clara sobre o que se aplica e o que se propõe;
- o paralelismo tem donos explícitos por arquivo, artefato e recurso;
- a escrita separa obrigação de liberdade, e regras compostas viraram itens.

### Estrutura

- A v5 substitui a v4 na raiz, com a mesma árvore: `AGENTS.md`, `CLAUDE.md`, `.claude/`, `.codex/` e `pipeline/`.
- `pipeline/` continua plana. Entram dois arquivos:
  - `evolucao.md`: quando a pipeline muda e com que autoridade;
  - `backlog.md`: achados fora do escopo, sobras não críticas da revisão, propostas pendentes e pendências adiadas.
  - Por quê: doze arquivos não pedem pastas. A autoridade de cada arquivo fica numa lista única, em `evolucao.md › Aplicar ou propor`.
  - Alternativa descartada: pastas por autoridade (`processo/`, `registros/`). Simplificaria os globs de permissão, mas alongaria cada citação de ficha e revisão.
- `escrita.md` continua separado de `evolucao.md`.
  - Por quê: `escrita.md` responde "como escrever" e serve também para fichas e briefs; `evolucao.md` responde "posso mudar isto?". São perguntas de momentos diferentes.

### Decisões principais

#### Autonomia do orquestrador

- Pergunta só em três casos: irreversível ou de alto impacto, ambiguidade que muda o resultado, informação que só o humano tem (`orquestracao.md › Autonomia`).
- Ambiguidade só é pergunta quando não há leitura claramente melhor e as leituras levam a entregas diferentes. Isso preserva o "há leitura razoável → decida" da v4.
- Toda decisão tomada sem perguntar, entre alternativas que o humano poderia ter escolhido diferente, é registrada com o motivo na entrega, no brief do revisor e no corpo do commit.
  - Por quê: a v4 dizia "se relevante, vira linha na entrega", sem critério de relevância e sem registro durável. O commit é o registro que dura sem criar um arquivo de histórico.
  - Alternativa descartada: um `decisoes.md`. Cresceria sem limite e duplicaria o `git log`; decisões que outras tarefas repetem já têm lugar em `padroes.md`.
- Instalar uma biblioteca de `stack.md` não pede autorização; dependência fora dela é pergunta.
  - Por quê: o humano já escolheu a stack. Na v4, qualquer dependência nova era pergunta, o que contrariava essa escolha.

#### Achados de revisão

- O revisor classifica a gravidade: `crítico` (critério, defeito, segurança, norma ou proteção) ou `desvio` (desvio arquitetural que nenhuma norma proíbe).
- O orquestrador faz a triagem da causa antes de corrigir: `implementação`, `ficha`, `pipeline` ou `indeterminada` (`orquestracao.md › Causa dos achados`).
  - Por quê o orquestrador: só ele vê ao mesmo tempo a ficha, as normas e o achado. O revisor não recebe a ficha, por desenho, e o implementador julgaria o próprio trabalho.
  - Por quê `ficha` como causa própria: sem ela, um erro do orquestrador na ficha seria lançado como erro do implementador (e subiria o nível à toa) ou como erro de norma (e mudaria uma norma que estava certa). A v4 já tratava a ficha ambígua como "não é falha"; a v5 só dá nome a isso.
  - Para usar a causa `implementação`, o orquestrador cita o trecho violado e onde o implementador o tinha. Isso evita culpar o implementador por padrão.
  - Alternativa descartada: um agente triador. Precisaria receber ficha, normas e achado, que o orquestrador já tem, e custaria mais uma instância por revisão.
- O revisor ganha o campo opcional `Pipeline:`, para apontar norma ambígua ou ausente. Ele lê as normas como um implementador as leria, sem o contexto da implementação, e por isso é o melhor detector de ambiguidade. Para o orquestrador, o campo é indício, não prova.
- A causa `indeterminada` é registrada em `impactos/`. A segunda ocorrência do mesmo tipo passa a ser `pipeline`.
  - Por quê: sem memória entre sessões, a recorrência só aparece se a primeira ocorrência estiver escrita.
- Limite de dois ciclos por tarefa: revisão completa e, se a correção foi crítica ou substancial, uma conferência só dos achados e das correções.
  - Crítico no que a tarefa mudou é sempre corrigido, inclusive depois do limite. Nesse caso, quem confirma a correção é o orquestrador, sem terceiro revisor.
  - Não crítico que sobra vai para o backlog.
  - Por quê: o limite fecha o loop; a exceção para crítico impede que ele vire desculpa para entregar defeito.
- Achado em código que a tarefa não tocou vai para o backlog e não bloqueia a entrega. Se for crítico, a entrega o leva como pergunta, com recomendação.
  - Por quê: corrigir código fora da mudança amplia o escopo, pode colidir com outras fichas e contraria a regra de legado ("não o corrija fora do escopo"). Leitura adotada: "críticos sempre são corrigidos" vale para o que a tarefa mudou.

#### Normas proativas

- A checagem de cobertura acontece antes de delegar (`orquestracao.md › Cobertura da pipeline`): dependência ainda não usada, primeiro artefato de um tipo, integração nova, ferramenta nova, área sem escolha fechada.
  - Por quê: norma escrita depois que os implementadores decidiram chega tarde.
- Uma biblioteca nova costuma pedir duas entradas: uma norma antes (fecha a escolha) e um padrão depois da primeira instância (registra a forma).
- Autoridade em duas listas fechadas (`evolucao.md › Aplicar ou propor`):
  - aplica e declara: norma nova aditiva e sem conflito, padrões, particularidades, backlog, fatos de `projeto.md`, manutenção de norma que não muda o que ela exige;
  - propõe e aguarda: alterar ou remover norma, norma nova com conflito, qualquer mudança de processo, de `stack.md` ou de definições de agente.
- "Aditiva e sem conflito" tem definição verificável: não contradiz nem restringe entrada existente, não escolhe entre formas que já convivem e não cria legado.
- Pedido explícito do humano para mudar uma norma já é a aprovação. Conflito implícito entre o pedido e uma norma é pergunta.
  - Por quê: a v4 deixava o orquestrador mudar qualquer norma "no mesmo trabalho e declarar". A v5 separa o que o humano pediu do que o orquestrador inferiu.
- `normas.md` sai da lista `ask` de `.claude/settings.json` e da lista de protegidos.
  - Por quê: com o gate, toda norma nova aditiva pediria confirmação, o que anula a autonomia que o princípio concede. A regra de autoridade em `evolucao.md` vale igual no Claude Code e no Codex, que não tem esse gate. A conferência do diff continua impedindo que um subagente escreva ali.
  - Alternativa descartada: manter o gate. É mais seguro contra uma alteração rotulada por engano como aditiva, mas transforma toda norma nova em pergunta.

#### Delegação e paralelismo

- O `t0` é definido pelos três fechamentos: entrada, saída e aceite. Localizar e listar ocorrências entra como exemplo de tarefa mecânica.
- Os níveis viram uma escada conferida em ordem; vale o menor nível que dá conta de todo o julgamento da ficha.
- Donos explícitos (`orquestracao.md › Donos`): a ficha é dona dos seus arquivos, artefatos e recursos exclusivos do disparo até a conferência. Ninguém mais escreve ali, nem o orquestrador. O mapa de donos é montado antes de cada onda.
- O implementador devolve bloqueio se um arquivo seu mudar sem que ele o tenha escrito: é o sinal de que a regra de donos foi violada.
- Alternativa descartada: um worktree por ficha. Isolaria as escritas, mas a integração viraria merge, e comandos que usam recursos compartilhados (lock, banco, portas) continuariam colidindo.

#### Escrita

- `escrita.md` abre com o princípio "clareza não é brevidade", com um exemplo, e com um vocabulário fixo: frase imperativa é obrigação, `Livre:` ou "pode" com condição é liberdade, `Por quê:` só quando não é óbvio.
- Regras compostas da v4 viraram itens, sem perder conteúdo. A precedência entre fontes virou lista numerada.
- O `Registro` do implementador ganhou rótulos (`lacuna`, `norma ambígua`, `norma conflitante`...) que alimentam a triagem e `evolucao.md`.
- Contradições da v4 resolvidas:
  - "faça a etapa você mesmo" × "não escreva código do produto";
  - "nenhum arquivo guarda histórico" × `impactos/`;
  - "não há segunda rodada" × "pergunte uma vez" no imprevisto.

### O que não mudou

- `normas.md`: as normas COD e UI, sem alteração.
- `stack.md`: a tabela de bibliotecas.
- Modelos e esforço de cada nível no Claude Code e no Codex, e a lista fechada de `tools`.
- Conferência pelo diff contra a linha de base, escalonamento por causa, terceira falha leva a entrega parcial.
- Git direto na branch principal, commit só pelo orquestrador, memória de agente desligada.

### Migração de um projeto na v4

- Substitua pelos da v5: `AGENTS.md`, `CLAUDE.md`, as definições em `.claude/agents/` e `.codex/agents/`, e `pipeline/orquestracao.md`, `ficha.md`, `revisao.md`, `escrita.md`, `adocao.md` e `stack.md`.
- Acrescente `pipeline/evolucao.md` e `pipeline/backlog.md`, este só com as seções.
- Mantenha os registros do projeto: `normas.md`, `padroes.md`, `particularidades.md` e `impactos/`.
- Em `projeto.md`, mantenha o conteúdo do projeto e mude só:
  - `Arquivos protegidos`: a lista explícita de `pipeline/` da v5, sem `normas.md` e com `evolucao.md`;
  - `Paralelismo`: tire a regra de falta de vagas, que foi para `orquestracao.md`.
- Em `.claude/settings.json`, junte às regras do projeto as mudanças da v5: sai `Edit(/pipeline/normas.md)`, entra `Edit(/pipeline/evolucao.md)`.
