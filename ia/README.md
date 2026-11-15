# A pipeline, para pessoas

A sessão principal do Claude Code ou do Codex age como tech lead do seu pedido: entende, planeja, encomenda o trabalho a executores, confere cada retorno pelo diff, chama um auditor independente quando há risco e entrega com as escolhas declaradas.

## Onde achar

| O que você procura                   | Onde                                 |
| ------------------------------------ | ------------------------------------ |
| Instalar, rodar e checar a aplicação | `README.md`, na raiz                 |
| O que existe e como foi feito        | o código: uma pasta por unidade      |
| As regras que os agentes seguem      | `ia/regras/`, um arquivo por assunto |
| O que ficou para depois              | `ia/pendencias.md`                   |
| Por que algo mudou, inclusive regras | `git log`                            |

`ia/` não repete o código: guarda só decisões, limites e armadilhas que ele não mostra. Não há catálogo de componentes nem de funções.

## Como usar

- Abra a ferramenta na raiz e peça em linguagem natural. Pergunta é respondida direto, sem encomendas.
- Ela só pergunta o que é caro de desfazer, o que é ambíguo de um jeito que muda o resultado, ou o que só você sabe. Uma rodada, com opções e recomendação.
- A entrega começa por `Concluído.`, `Parcial.` ou `Preciso de uma decisão.` e lista só o que você precisa decidir ou não acharia no diff.
- Aceitar a entrega aprova o que foi declarado. Recusou algo: diga, e é desfeito.
- Para criar um hábito, diga "a partir de agora, sempre X": vira regra ou checagem na hora.
- O commit sai quando você pede.

## Estrutura

```text
AGENTS.md            o único arquivo sempre carregado: papéis, leis, tabela de regras
CLAUDE.md            importa o AGENTS.md no Claude Code
.claude/  .codex/    agentes (modelo e esforço de cada nível), permissões e protegidos
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
  regras/            regras e alertas, lidos só pelo assunto que o arquivo aciona
  fatos.md           o que só agente usa para operar
  pendencias.md      o que ficou para depois
```

## Como ela se corrige

- Gatilho: você corrige um comportamento ou dá uma instrução duradoura; ou uma instrução causa um problema, ou um problema se repete. Tarefa que correu bem não muda `ia/`.
- Reparo: o primeiro remédio que serve, nesta ordem: nada, menos texto, checagem ou código, posição da instrução, texto novo, você.
- Só com você: mudar o que uma regra exige, a tabela de bibliotecas, as leis e a configuração dos agentes.

O procedimento inteiro está em `quando/reparo.md`.

## Sinais de saúde

- `ia/` mudando em toda tarefa, ou assunto perto do teto de linhas: texto entrando onde cabia checagem, ou nada.
- Regra ou alerta com nome de função, prop ou caminho que se acha na árvore: transcrição do código.
- Bloqueios ou subidas de nível frequentes: encomendas mal fechadas, nível baixo demais, ou falta a regra que decide.
- `Dívida:` crescendo sem migração, ou propostas velhas em pendências: decisões esperando por você.
- Orquestrador escrevendo código do produto, ou encomenda com código da solução: saiu do papel.
- Auditorias que sempre aprovam mudanças grandes: o pedido de auditoria pode estar levando o raciocínio de quem fez.

Nada aqui é verificado por script: cada informação mora num lugar só, e quem muda um título ou caminho busca as citações.
