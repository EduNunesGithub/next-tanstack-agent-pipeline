# Pipeline v6

> Para: pessoas · Leia quando: para entender e operar a pipeline.

A sessão principal do Claude Code ou do Codex age como tech lead do seu pedido. Ela entende o que você quer, desenha a solução, entrega missões com arquivos de posse exclusiva a implementadores de cinco níveis, confere cada resultado pelo diff, chama um revisor independente quando há risco e entrega com as decisões declaradas.

## Como usar

- Abra o Claude Code ou o Codex na raiz do repositório e peça em linguagem natural. Pergunta e pedido de explicação são respondidos direto, sem missões.
- O orquestrador só pergunta o que é caro de desfazer, o que é ambíguo de um jeito que muda o resultado, ou o que só você sabe. As perguntas vêm numa rodada só, cada uma com opções e uma recomendação.
- A entrega começa pelo estado (`Concluído.`, `Entrega parcial.` ou `Preciso de uma decisão.`) e lista as decisões tomadas sem perguntar, as mudanças na pipeline, o que foi para o backlog e como foi verificado.
- Aceitar a entrega aprova as mudanças aplicadas e declaradas. Uma proposta de mudança na pipeline só vale com a sua aprovação explícita.
- Para criar um hábito, diga "a partir de agora, sempre X": vira regra ou padrão, e o pedido já conta como aprovação.
- O commit é feito quando você pede, depois de aceitar a entrega.

## Estrutura

```text
AGENTS.md                    papéis, leis, conflitos, glossário e mapa (todo agente lê)
CLAUDE.md                    importa o AGENTS.md no Claude Code
.claude/  .codex/            definições dos agentes e configurações
pipeline/
  papeis/                    o contrato de cada papel: orquestrador, implementador, revisor
  guias/                     paralelismo, revisão, falhas, evolução, escrita e adoção, por gatilho
  conhecimento/              índice e áreas: fontes, regras, padrões e armadilhas
  projeto.md                 fatos do projeto que o código não mostra
  backlog.md                 achados, propostas e pendências
  ocorrencias/               vezes em que a pipeline falhou
```

## Quem lê o quê

| Papel         | Lê                                                   |
| ------------- | ---------------------------------------------------- |
| Orquestrador  | `AGENTS.md`, o próprio papel, `projeto.md`, as áreas |
| Implementador | `AGENTS.md`, o próprio papel, o índice, as áreas     |
| Revisor       | `AGENTS.md`, o próprio papel, o índice, as áreas     |

- As áreas lidas são as que os arquivos do trabalho acionam pelos gatilhos do índice; a de código vale sempre.
- O orquestrador lê um guia só quando o gatilho dele dispara. Uma tarefa de uma missão, sem risco, não lê nenhum.

## Níveis

| Nível | O que cabe ao implementador decidir            |
| ----- | ---------------------------------------------- |
| `t0`  | nada que mude o resultado: execução fechada    |
| `t1`  | adaptar uma forma que o projeto já mostra      |
| `t2`  | uma solução convencional sem exemplar          |
| `t3`  | estrutura: contratos, persistência, integração |
| `t4`  | segurança, concorrência, migração, desempenho  |

O modelo e o esforço de cada nível estão nas definições de `.claude/agents/` e `.codex/agents/`.

## Conferência

A pipeline não tem script de verificação. A cada mudança nela, o orquestrador faz a conferência de `pipeline/guias/escrita.md`: referências, caminhos, mapa e cabeçalhos, índice e IDs, protegidos e regras `ask`, paridade dos agentes.

## Sinais de saúde

- Referência quebrada, mapa diferente do cabeçalho ou protegido sem regra `ask`: a pipeline foi editada sem conferência. Corrija antes da próxima tarefa.
- Devoluções frequentes do mesmo tipo: missões mal fechadas ou uma área sem a regra que decide.
- Ocorrências parecidas se repetindo: uma instrução não está evitando o erro.
- Subidas de nível frequentes: classificação baixa demais ou divisão ruim das missões.
- Missão com código ou com a implementação descrita: microgestão; o implementador perde o julgamento que justifica o nível dele.
- Achados de consistência recorrentes na mesma área: falta um padrão.
- `Legado:` crescendo sem migração: o backlog precisa de uma decisão sua.
- Propostas antigas no backlog: decisões esperando por você.
- O orquestrador escrevendo código do produto: ele saiu do papel.
- Revisões que sempre aprovam mudanças grandes: o brief pode estar levando o raciocínio da implementação.

## Adoção

Para usar a pipeline num projeto novo, num projeto que já existe ou num projeto que estava na v5, peça à sessão principal; ela segue `pipeline/guias/adocao.md`.
