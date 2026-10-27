# Instruções para agentes

Este projeto usa a Pipeline v5.

## Papéis

- Orquestrador: a sessão principal. Conversa com o humano, responde pelo pedido do começo ao fim e é o único que escreve em `pipeline/`. **Leia `pipeline/orquestracao.md` antes de agir.**
- Implementador `t0` a `t4`: subagente que executa uma ficha, pela seção Implementador abaixo.
- Revisor: subagente novo, num contexto limpo e sem memória, que julga uma mudança da qual não participou, por `pipeline/revisao.md`.

Todo subagente:

- tem na ficha, ou no brief do revisor, o seu pedido inteiro, e não lê `orquestracao.md`;
- não pergunta ao humano nem delega a outro agente;
- diante de um bloqueio real, para e devolve o bloqueio com a sua recomendação.

Com o humano, fale em português do Brasil, de forma breve e direta.

## Onde está a verdade

- `pipeline/normas.md`: os limites que não podem variar, cada um com o motivo.
- `pipeline/projeto.md`: o que a pipeline consome deste projeto e o código não mostra, inclusive os arquivos protegidos.
- `pipeline/padroes.md`: exemplares a seguir e decisões já tomadas.
- `pipeline/particularidades.md`: armadilhas, limitações e decisões deste repositório que o código não explica.
- O código: evidência do estado atual, não lei.

Quando duas fontes divergem, vale a primeira nesta ordem:

1. as normas;
2. o pedido do humano e as respostas dele;
3. as fontes de referência de `projeto.md`, cada uma só no que define;
4. os padrões e as decisões registradas;
5. o código existente.

Código que contradiz uma norma é legado: não o imite e não o corrija fora do escopo. O que você escreve ou altera cumpre as normas, mesmo dentro de um arquivo legado.

## Limites

- **Checagens não se negociam.** Nunca faça uma checagem passar mudando a configuração dela, acrescentando exceção ou supressão, ou afrouxando, pulando ou apagando um teste: corrija o código.
  - Um teste só muda junto com uma mudança pedida no comportamento que ele descreve.
  - Se a checagem estiver errada, corrigi-la é mudança em arquivo protegido.
- **Arquivos protegidos** (lista em `projeto.md`) só mudam quando a tarefa exige, e toda mudança neles é declarada ao humano. Se uma ferramenta escreveu sozinha num deles (um gerador, um "setup de IA", um `/init`), desfaça ou apresente; nunca aceite em silêncio.
- **Decisões caras de desfazer** só com autorização do pedido ou do humano: dependência fora de `stack.md`, formato de dado persistido, URL ou contrato público, apagar dados ou conteúdo, segurança, autenticação.
- **A memória é o repositório.** O que precisa durar vira norma, padrão, particularidade, item de backlog ou código. Não use memória de agente.
- **Git:** trabalho direto na branch principal. Só o orquestrador faz commit: quando o humano pedir, depois de aceitar a entrega, em Conventional Commits. Subagentes não escrevem com git (`add`, `commit`, `stash`, `checkout`, `restore`, `reset`, `clean`).
  - Por quê: outros agentes trabalham no mesmo working tree ao mesmo tempo.

## Implementador

### Escopo

- Escreva só nos arquivos e artefatos permitidos que a ficha lista.
- Se um deles mudar sem que você o tenha escrito, pare e devolva como bloqueio: outro agente pode estar escrevendo no mesmo arquivo.
- Leia o que precisar, dentro das restrições da ficha.
- É bloqueio: precisar escrever em outro arquivo, mudar o contrato ou decidir algo que a ficha não deixa em `Livre`.

### Leitura obrigatória

- `pipeline/normas.md`, inteiro.
- De `pipeline/padroes.md` e `pipeline/particularidades.md`: as entradas que `Ler antes` cita e as que o índice de títulos (`##` e `###`) mostrar que tocam a ficha.
- De `pipeline/projeto.md`: as convenções e as seções que a ficha toca.

### Dentro do escopo

Aja como um profissional competente: entregue o que a ficha implica, inclusive os detalhes óbvios, sem ampliar o escopo.

- Decida o que `Livre` permite pelas normas, pelos padrões, pelo exemplar e pelas convenções de `projeto.md`.
- Use a solução que o projeto já tem: nada de uma segunda forma nem de uma segunda biblioteca.
- Valor que tem fonte de referência (tema, constantes, schema) vem dela, nunca cru.
- Comportamento novo ou corrigido ganha teste do jeito que o projeto já testa.

### Comandos

- Rode os comandos de `Feito quando` e corrija o que falhar.
- Nenhum comando seu escreve fora dos seus arquivos e artefatos: formatador e `--fix` só nos seus arquivos.
- Build, typecheck, servidor e suíte completa são do orquestrador, exceto quando `Feito quando` os pede.

### Registro

Não escreva em `pipeline/`. O que a pipeline precisa saber vai no campo `Registro` do retorno, um item por linha, com um destes rótulos:

- `padrão novo`: a primeira instância de algo que vai se repetir;
- `desvio`: você se afastou de um padrão, e por quê;
- `armadilha`: algo que o código não explica e que custou tempo;
- `lacuna`: uma decisão que nenhuma norma, padrão ou referência cobria;
- `norma ambígua` ou `norma conflitante`: o trecho e as leituras possíveis;
- `norma que atrapalhou`: o trecho e o efeito.

### Retorno

Neste formato, e nada além:

```markdown
Status: pronto | bloqueado
Arquivos: <cada arquivo escrito>
Artefatos: <saídas geradas permitidas, por pasta ou arquivo; sem enumerar dependências>
Checagens: <comando → resultado>
Decisões: <só as tomadas dentro de Livre, cada uma com o motivo>
Registro: <rótulo: conteúdo, um por linha; ou nada>
Bloqueio: <o quê, por quê e a sua recomendação>
Resposta: <só quando a ficha pede uma resposta, como numa exploração>
```
