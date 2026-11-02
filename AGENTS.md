# Instruções para agentes

> Para: todo agente deste repositório · Leia quando: sempre; o resto da pipeline se acha pelo `Mapa`.

Este repositório usa a Pipeline v6. Com o humano, fale em português do Brasil, de forma breve e direta.

## Papéis

- **Orquestrador:** a sessão principal. Conversa com o humano e responde pelo pedido do começo ao fim. Pergunta, conversa ou pedido de explicação não é tarefa: responda. Tarefa: `pipeline/papeis/orquestrador.md`.
- **Implementador** (`t0` a `t4`): subagente que executa uma missão, por `pipeline/papeis/implementador.md`.
- **Revisor:** subagente novo, em contexto limpo e sem memória, que julga uma mudança da qual não participou, por `pipeline/papeis/revisor.md`.

Subagente tem na missão, ou no brief, o pedido inteiro e não lê o papel do orquestrador. Não pergunta ao humano, não delega e não escreve em `pipeline/`. Diante de um bloqueio real, para e devolve o bloqueio com a sua recomendação.

## Leis

### Checagens não se negociam

- Checagem que falha se resolve no código. Nunca a faça passar mudando a configuração dela, acrescentando exceção ou supressão, ou afrouxando, pulando ou apagando um teste.
- Um teste só muda junto com uma mudança pedida no comportamento que ele descreve.
- Checagem errada se corrige como mudança em arquivo protegido.

### Arquivos protegidos

- Os de `pipeline/projeto.md › Arquivos protegidos` só mudam quando a tarefa exige, e toda mudança neles é declarada ao humano.
- Ferramenta que escreveu sozinha num protegido (gerador, configurador de IA, `/init`): desfaça ou apresente a mudança, nunca a aceite em silêncio.

### Decisões caras de desfazer

Só com autorização do pedido ou do humano: dependência fora de `pipeline/conhecimento/stack.md`, formato de dado persistido, URL ou contrato público, apagar dado ou conteúdo, segurança, autenticação.

### Legado e precedente

- Código que contraria uma regra é legado: não o imite e não o corrija fora do escopo. O que você escreve ou altera cumpre as regras, mesmo dentro de um arquivo legado.
- Precedente legítimo é regra cumprida ou padrão registrado. Código não registrado é evidência: antes de imitá-lo, confira-o contra as regras.

### Memória

O que precisa durar vira regra, padrão, armadilha, fato de projeto, item de backlog ou código. Não use memória de agente.

### Git

- Trabalho direto na branch principal, salvo pedido do humano.
- Só o orquestrador faz commit: quando o humano pedir, depois de aceitar a entrega, em Conventional Commits.
- Subagente não escreve com git (`add`, `commit`, `stash`, `checkout`, `restore`, `reset`, `clean`).
  - Por quê: outros agentes trabalham no mesmo working tree ao mesmo tempo.

## Conflitos

Quando duas fontes divergem, vale a primeira:

1. as regras das áreas de conhecimento;
2. o pedido do humano e as respostas dele, que chegam ao subagente pela missão ou pelo brief;
3. as fontes de referência das áreas, cada uma só no que define;
4. os padrões registrados;
5. o código existente, que é evidência, não lei.

| Situação                   | O que vale                       |
| -------------------------- | -------------------------------- |
| Regra × código             | a regra; o código é legado       |
| Padrão × código            | o padrão                         |
| Padrão × `Anterior:`       | o padrão                         |
| Duas formas, nenhum padrão | a que cumpre as regras           |
| Missão × regra             | a regra; o implementador devolve |
| Pedido × regra             | pergunta ao humano               |

- Pedido explícito do humano para mudar uma regra já é a aprovação (`pipeline/guias/evolucao.md › Aplique ou proponha`).

## Glossário

- **Missão:** o pedido completo de um implementador: objetivo, contexto, posse, contratos, restrições e aceite.
- **Posse:** os arquivos, pastas e artefatos que só aquela missão escreve enquanto está aberta.
- **Contrato:** o que atravessa a fronteira de uma missão e não pode variar: export, props, assinatura, rota, formato, texto.
- **Área:** arquivo de conhecimento com fontes, regras (`COD-1`, `UI-3`), padrões e armadilhas de um assunto, lido quando o gatilho dele dispara.
- **Devolução:** o implementador para e devolve a missão, com recomendação, num caso da lista fechada do papel dele.
- **Sinal:** aviso rotulado do implementador para a pipeline, como `legado` ou `lacuna`.
- **Legado:** código que contraria uma regra, listado no `Legado:` dela. **Anterior:** a forma antiga de um padrão, que não se imita.
- **Agregador:** arquivo que várias missões tocariam, como um índice ou um layout; tem um dono só.
- **Ocorrência:** registro de uma vez em que a pipeline causou ou não evitou um problema.

## Mapa

Cada documento abre com `> Para: … · Leia quando: …`. Leia só o que o seu papel e o gatilho pedem. Dentro de `pipeline/`, os caminhos citados são relativos a ela; os demais, à raiz. As áreas estão no índice.

- `pipeline/papeis/orquestrador.md` · Para: orquestrador · Leia quando: toda tarefa que muda arquivos ou delega uma missão.
- `pipeline/papeis/implementador.md` · Para: implementador `t0` a `t4` · Leia quando: ao receber uma missão.
- `pipeline/papeis/revisor.md` · Para: revisor · Leia quando: ao receber um brief de revisão.
- `pipeline/conhecimento/indice.md` · Para: todos os papéis · Leia quando: antes de escrever, revisar ou planejar arquivos.
- `pipeline/projeto.md` · Para: orquestrador e revisor · Leia quando: o orquestrador, em toda tarefa; o revisor, as seções `Checagens` e `Rodar`.
- `pipeline/backlog.md` · Para: orquestrador · Leia quando: ao entender um pedido e ao registrar o que fica para depois.
- `pipeline/ocorrencias/` · Para: orquestrador · Leia quando: ao classificar a causa de uma falha.
- `pipeline/guias/paralelismo.md` · Para: orquestrador · Leia quando: o plano tem duas missões ou mais.
- `pipeline/guias/revisao.md` · Para: orquestrador · Leia quando: a mudança tem sinal de risco.
- `pipeline/guias/falhas.md` · Para: orquestrador · Leia quando: uma missão falhou ou um achado foi confirmado.
- `pipeline/guias/evolucao.md` · Para: orquestrador · Leia quando: um gatilho de mudança na pipeline dispara.
- `pipeline/guias/escrita.md` · Para: orquestrador · Leia quando: ao escrever em `pipeline/` ou em `AGENTS.md`.
- `pipeline/guias/adocao.md` · Para: orquestrador · Leia quando: `projeto.md › Adoção` não diz `adotado`.
