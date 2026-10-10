# Instruções para agentes

Este projeto usa a Pipeline v4.

| Papel | Quem | Segue |
| --- | --- | --- |
| Orquestrador | a sessão principal: conversa com o humano, decide, divide em fichas, delega, confere e entrega | este arquivo e `pipeline/orquestracao.md` |
| Implementador `t0` a `t3` | subagente que executa uma ficha | este arquivo e a ficha (`pipeline/ficha.md`) |
| Revisor | subagente novo, num contexto limpo e sem memória, que julga uma mudança da qual não participou | este arquivo e `pipeline/revisao.md` |

Modelo e esforço de cada agente: na definição dele, em `.claude/agents/` e `.codex/agents/`.

**Se você é a sessão principal, leia `pipeline/orquestracao.md` antes de agir.** Se você é um subagente, não a leia: a ficha (ou o brief do revisor) é o seu pedido. Não pergunte ao humano nem delegue a outro agente; diante de um bloqueio real, pare e devolva o bloqueio com a sua recomendação.

Com o humano, fale em português do Brasil, de forma breve e direta.

## Onde está a verdade

- `pipeline/normas.md`: os limites que não podem variar, cada um com o motivo. Só muda com aprovação do humano.
- `pipeline/projeto.md`: convenções, fontes de referência, checagens, paralelismo, como rodar e observar o produto, arquivos protegidos. Só muda com aprovação do humano.
- `pipeline/padroes.md`: exemplares a seguir e decisões já tomadas. O orquestrador mantém.
- O código: evidência do estado atual, não lei.

Cada regra fica só na sua fonte, sem ser repetida ou resumida em outro arquivo.

Quando duas fontes divergem, vale a primeira nesta ordem: (1) as normas; (2) o pedido do humano e as respostas dele; (3) as fontes de referência, cada uma só no que define; (4) os padrões e as decisões registradas; (5) o código existente.

Código que contradiz uma norma é legado: não o imite e não o corrija fora do escopo. O que você escreve ou altera cumpre as normas, mesmo dentro de um arquivo legado.

## Limites

- **Checagens não se negociam.** Nunca faça uma checagem passar mudando a configuração dela, acrescentando exceção ou supressão, ou afrouxando, pulando ou apagando um teste: corrija o código. Um teste só muda junto com uma mudança pedida no comportamento que ele descreve. Se a checagem estiver errada, corrigi-la é mudança em arquivo protegido.
- **Arquivos protegidos** (lista em `projeto.md`) só mudam quando a tarefa exige, e toda mudança neles é declarada ao humano. Se uma ferramenta escreveu sozinha num deles (um gerador, um "setup de IA", um `/init`), desfaça ou apresente; nunca aceite em silêncio.
- **Decisões caras de desfazer** (dependência nova, formato de dado persistido, URL ou contrato público, apagar dados ou conteúdo, segurança, autenticação) só com autorização do pedido ou do humano.
- **A memória é o repositório.** O que precisa durar vira norma, padrão ou código. Não use memória de agente.
- **Git:** trabalho direto na branch principal. Só a sessão principal faz commit: quando o humano pedir, depois de aceitar a entrega, em Conventional Commits. Subagentes não escrevem com git (`add`, `commit`, `stash`, `checkout`, `restore`, `reset`, `clean`): outros agentes trabalham no mesmo working tree ao mesmo tempo.

## Implementador

- **Escopo:** escreva só nos arquivos que a ficha lista; ler é livre. Se precisar escrever em outro arquivo, mudar o contrato ou decidir algo que a ficha não deixa em `Livre`, isso é bloqueio.
- **Dentro do escopo**, aja como um profissional competente: decida o que `Livre` permite pelas normas, pelos padrões, pelo exemplar e pelas convenções de `projeto.md`. Entregue o que a ficha implica, inclusive os detalhes óbvios, sem ampliar o escopo. Use a solução que o projeto já tem: nada de uma segunda forma nem de uma segunda biblioteca. Valor que tem fonte de referência (tema, constantes, schema) vem dela, nunca cru. Comportamento novo ou corrigido ganha teste do jeito que o projeto já testa.
- **Comandos:** rode os de `Feito quando` e corrija o que falhar. Nenhum comando seu pode escrever fora dos seus arquivos: formatador e `--fix` só nos seus arquivos; build, typecheck, servidor e suíte completa são do orquestrador.
- **Registro:** não escreva em `pipeline/`. A primeira instância de algo que vai se repetir, um desvio de padrão ou uma norma que atrapalhou vão no campo `Registro` do retorno.
- **Retorno:** no formato de `pipeline/ficha.md`, e nada além.
