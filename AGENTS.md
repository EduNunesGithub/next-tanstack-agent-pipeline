# Instruções para agentes

Este projeto usa a Pipeline v4.

- Orquestrador: a sessão principal, que conversa com o humano e responde pelo pedido. **Leia `pipeline/orquestracao.md` antes de agir.**
- Implementador `t0` a `t4`: subagente que executa uma ficha.
- Revisor: subagente novo, num contexto limpo e sem memória, que julga uma mudança da qual não participou, por `pipeline/revisao.md`.

Subagente não lê `orquestracao.md`: a ficha (ou o brief do revisor) é o seu pedido. Não pergunte ao humano nem delegue a outro agente; diante de um bloqueio real, pare e devolva o bloqueio com a sua recomendação.

Com o humano, fale em português do Brasil, de forma breve e direta.

## Onde está a verdade

- `pipeline/normas.md`: os limites que não podem variar, cada um com o motivo.
- `pipeline/projeto.md`: o que a pipeline consome deste projeto e o código não mostra, inclusive os arquivos protegidos.
- `pipeline/padroes.md`: exemplares a seguir e decisões já tomadas.
- `pipeline/particularidades.md`: armadilhas, limitações e decisões deste repositório que o código não explica.
- O código: evidência do estado atual, não lei.

Quando duas fontes divergem, vale a primeira nesta ordem: (1) as normas; (2) o pedido do humano e as respostas dele; (3) as fontes de referência, cada uma só no que define; (4) os padrões e as decisões registradas; (5) o código existente.

Código que contradiz uma norma é legado: não o imite e não o corrija fora do escopo. O que você escreve ou altera cumpre as normas, mesmo dentro de um arquivo legado.

## Limites

- **Checagens não se negociam.** Nunca faça uma checagem passar mudando a configuração dela, acrescentando exceção ou supressão, ou afrouxando, pulando ou apagando um teste: corrija o código. Um teste só muda junto com uma mudança pedida no comportamento que ele descreve. Se a checagem estiver errada, corrigi-la é mudança em arquivo protegido.
- **Arquivos protegidos** (lista em `projeto.md`) só mudam quando a tarefa exige, e toda mudança neles é declarada ao humano. Se uma ferramenta escreveu sozinha num deles (um gerador, um "setup de IA", um `/init`), desfaça ou apresente; nunca aceite em silêncio.
- **Decisões caras de desfazer** (dependência nova, formato de dado persistido, URL ou contrato público, apagar dados ou conteúdo, segurança, autenticação) só com autorização do pedido ou do humano.
- **A memória é o repositório.** O que precisa durar vira norma, padrão ou código. Não use memória de agente.
- **Git:** trabalho direto na branch principal. Só a sessão principal faz commit: quando o humano pedir, depois de aceitar a entrega, em Conventional Commits. Subagentes não escrevem com git (`add`, `commit`, `stash`, `checkout`, `restore`, `reset`, `clean`): outros agentes trabalham no mesmo working tree ao mesmo tempo.

## Implementador

- **Escopo:** escreva só nos arquivos e artefatos permitidos que a ficha lista; leia dentro das restrições do pedido. Se precisar escrever em outro arquivo, mudar o contrato ou decidir algo que a ficha não deixa em `Livre`, isso é bloqueio.
- **Leitura:** `normas.md` inteiro; de `padroes.md` e `particularidades.md`, o que `Ler antes` cita e o que mais o índice de títulos (`##` e `###`) mostrar que toca a ficha; de `projeto.md`, as convenções e as seções que a ficha toca.
- **Dentro do escopo**, aja como um profissional competente: decida o que `Livre` permite pelas normas, pelos padrões, pelo exemplar e pelas convenções de `projeto.md`. Entregue o que a ficha implica, inclusive os detalhes óbvios, sem ampliar o escopo. Use a solução que o projeto já tem: nada de uma segunda forma nem de uma segunda biblioteca. Valor que tem fonte de referência (tema, constantes, schema) vem dela, nunca cru. Comportamento novo ou corrigido ganha teste do jeito que o projeto já testa.
- **Comandos:** rode os de `Feito quando` e corrija o que falhar. Nenhum comando seu pode escrever fora dos arquivos e artefatos permitidos da ficha: formatador e `--fix` só nos seus arquivos. Fora o que `Feito quando` pedir, build, typecheck, servidor e suíte completa são do orquestrador.
- **Registro:** não escreva em `pipeline/`. A primeira instância de algo que vai se repetir, um desvio de padrão, uma armadilha que o código não explica ou uma norma que atrapalhou vão no campo `Registro` do retorno.
- **Retorno:** neste formato, e nada além:

  ```markdown
  Status: pronto | bloqueado
  Arquivos: <cada arquivo escrito>
  Artefatos: <saídas geradas permitidas, por pasta ou arquivo; sem enumerar dependências>
  Checagens: <comando → resultado>
  Decisões: <só as tomadas dentro de Livre>
  Registro: <padrão novo, desvio, armadilha ou norma que atrapalhou; ou nada>
  Bloqueio: <o quê, por quê e a sua recomendação>
  Resposta: <só quando a ficha pede uma resposta, como numa exploração>
  ```
