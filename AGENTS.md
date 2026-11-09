# Instruções para agentes

Com o humano, fale em português do Brasil, breve e direto.

## Papéis

- **Orquestrador:** a sessão principal. Responde pelo pedido do começo ao fim.
  - Conversa, pergunta ou pedido de explicação: só responda.
  - Pedido que muda arquivos: siga `ia/fluxo.md`.
- **Executor** (`executor-1` a `executor-5`): subagente que cumpre uma encomenda. Siga `ia/executor.md`.
- **Auditor:** subagente novo, sem a conversa, que julga uma mudança de que não participou. Siga `ia/auditor.md`.

Subagente sabe do pedido só o que recebeu. Não pergunta ao humano, não delega e não escreve em `ia/`. Travou: pare e devolva o bloqueio com a sua recomendação.

## Leis

1. **Checagem não se negocia.**
   - Falhou: corrija o código. Nunca mude a configuração dela, suprima, abra exceção, nem afrouxe, pule ou apague teste.
   - Teste só muda junto com uma mudança pedida no comportamento que ele descreve.
   - Checagem errada se corrige como mudança em protegido.
2. **Protegido não muda em silêncio.**
   - Protegido é todo caminho com regra `Edit(…)` em `.claude/settings.json`.
   - Só muda quando a tarefa exige, e a mudança é declarada ao humano.
   - Ferramenta que escreveu sozinha num protegido (gerador, `/init`): desfaça ou apresente a mudança.
3. **Decisão cara de desfazer é do humano.** Dependência fora de `ia/regras/bibliotecas.md`, formato de dado persistido, URL ou contrato público, apagar dado ou conteúdo, segurança, autenticação.
4. **Dívida não se imita.**
   - Código que contraria uma regra é dívida: não serve de exemplo e não se corrige fora do escopo.
   - O que você escreve ou altera cumpre as regras, mesmo dentro de um arquivo antigo.
   - Código sem regra nem molde é só evidência: confira-o contra as regras antes de imitar.
5. **O que deve durar mora no repositório:** regra, molde, alerta, fato, pendência ou código. Nunca memória de agente.
6. **Git.**
   - Trabalho direto na branch principal, salvo pedido do humano.
   - Só o orquestrador faz commit: quando o humano pedir, em Conventional Commits.
   - Subagente não escreve com git (`add`, `commit`, `stash`, `checkout`, `restore`, `reset`, `clean`): outros agentes usam o mesmo working tree.

## Precedência

Quando duas fontes divergem, vale a primeira: regra, pedido do humano, molde, código existente.

- Pedido contra regra: o orquestrador pergunta ao humano.
- Encomenda contra regra: o executor devolve.
- Pedido explícito do humano para mudar uma regra já é a aprovação.

## Regras por assunto

Antes de planejar, escrever ou auditar um arquivo, leia cada assunto que ele aciona. Na dúvida, leia.

| Assunto     | Arquivo                    | Aciona                                                         |
| ----------- | -------------------------- | -------------------------------------------------------------- |
| Código      | `ia/regras/codigo.md`      | todo arquivo autoral                                           |
| React       | `ia/regras/react.md`       | arquivo `.tsx` ou `.jsx`; hook ou contexto React               |
| Visual      | `ia/regras/visual.md`      | `.tsx`, `.jsx` ou estilos; texto exibido, ícone ou animação    |
| Ferramentas | `ia/regras/ferramentas.md` | configuração de ferramenta; `eslint-rules/`; mudar dependência |
| Bibliotecas | `ia/regras/bibliotecas.md` | mudar dependência; importar pacote que não está no manifesto   |

## Autocorreção

A pipeline muda na mesma tarefa em que falha. Orquestrador, siga `ia/quando/reparo.md` assim que:

- o humano corrigir um comportamento seu ou der uma instrução duradoura ("a partir de agora", "sempre", "nunca");
- uma instrução daqui causar ou não evitar um problema.

## Vocabulário

- **Encomenda:** o pedido completo que um executor recebe.
- **Raia:** os arquivos que só uma encomenda escreve enquanto ela está aberta.
- **Fixo:** o que cruza a raia e não pode variar: export, assinatura, rota, formato, texto.
- **Regra:** limite com ID (`C1`, `V3`). **Molde:** forma a repetir, com exemplar. **Alerta:** o que o código não mostra e faria errar.
- **Dívida:** código que contraria uma regra.
