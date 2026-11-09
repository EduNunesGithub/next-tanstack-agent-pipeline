# A pipeline, para pessoas

A sessão principal do Claude Code ou do Codex age como tech lead do seu pedido: entende, planeja, encomenda o trabalho a executores, confere cada retorno pelo diff, chama um auditor independente quando há risco e entrega com as escolhas declaradas.

## Como usar

- Abra a ferramenta na raiz e peça em linguagem natural. Pergunta é respondida direto, sem encomendas.
- Ela só pergunta o que é caro de desfazer, o que é ambíguo de um jeito que muda o resultado, ou o que só você sabe. Uma rodada, com opções e recomendação.
- A entrega começa por `Concluído.`, `Parcial.` ou `Preciso de uma decisão.` e lista escolhas, reparos na pipeline, pendências e como foi verificado.
- Aceitar a entrega aprova o que foi declarado. Recusou algo: diga, e é desfeito.
- Para criar um hábito, diga "a partir de agora, sempre X": vira regra ou molde na hora.
- O commit sai quando você pede.

## Estrutura

```text
AGENTS.md            o único arquivo sempre carregado: papéis, leis, tabela de regras
CLAUDE.md            importa o AGENTS.md no Claude Code
.claude/  .codex/    agentes, permissões e protegidos
ia/
  fluxo.md           o ciclo do orquestrador, em toda tarefa
  executor.md        o contrato de quem implementa
  auditor.md         o contrato de quem audita
  quando/            lido só quando o nome do arquivo acontece
    paralelo.md      duas encomendas ou mais
    risco.md         a mudança pede auditoria
    falha.md         uma encomenda falhou
    reparo.md        a pipeline errou, ou você a corrigiu
    inicio.md        o projeto ainda não adotou a pipeline
  regras/            regras, moldes e alertas, por assunto
  fatos.md           comandos, recursos e estado do projeto
  pendencias.md      o que ficou para depois
  diario.md          cada reparo, em uma linha
```

## Quem lê o quê

| Papel        | Sempre                                  | Só por gatilho         |
| ------------ | --------------------------------------- | ---------------------- |
| Orquestrador | `AGENTS.md`, `fluxo.md`, `fatos.md`     | `quando/`, os assuntos |
| Executor     | `AGENTS.md`, `executor.md`, a encomenda | os assuntos da raia    |
| Auditor      | `AGENTS.md`, `auditor.md`, `fatos.md`   | os assuntos do diff    |

## Níveis

| Agente       | O que resta decidir                           |
| ------------ | --------------------------------------------- |
| `executor-1` | nada: execução fechada                        |
| `executor-2` | adaptar uma forma que o projeto já mostra     |
| `executor-3` | uma solução convencional, sem exemplar        |
| `executor-4` | estrutura: fixos, persistência, integração    |
| `executor-5` | segurança, concorrência, migração, desempenho |

O modelo e o esforço de cada nível estão em `.claude/agents/` e `.codex/agents/`.

## Como ela se corrige

- Gatilho: você corrige um comportamento ou dá uma instrução duradoura; ou o orquestrador vê falha, retrabalho, pergunta desnecessária ou aviso de um subagente. Toda tarefa passa por essa pergunta antes da entrega.
- Reparo: acha a linha que deixou o problema acontecer, faz a menor mudança que remove a causa, registra uma linha no diário e declara na entrega.
- Recorrência: o mesmo sintoma de novo sobe a escada: texto, posição da instrução, checagem por ferramenta, você.
- Só com você: mudar o que uma regra exige, a tabela de bibliotecas, as leis e a configuração dos agentes.

O procedimento inteiro está em `quando/reparo.md`.

## Sinais de saúde

- Diário com o mesmo sintoma repetido: o reparo não está subindo a escada.
- Bloqueios frequentes do mesmo tipo: encomendas mal fechadas, ou falta a regra que decide.
- Subidas de nível frequentes: nível baixo demais ou divisão ruim.
- Encomenda com código da solução: microgestão.
- `Dívida:` crescendo sem migração, ou propostas velhas em pendências: decisões esperando por você.
- Orquestrador escrevendo código do produto: saiu do papel.
- Auditorias que sempre aprovam mudanças grandes: o pedido de auditoria pode estar levando o raciocínio de quem fez.

## Sem scripts

Nada aqui é verificado por script. A consistência vem do desenho: cada informação mora num lugar só, e quem muda um título ou caminho busca as citações.
