# Paralelo

O plano tem duas encomendas ou mais.

## Raias

- Cada arquivo, pasta, saída gerada e recurso exclusivo tem um dono por vez.
- A raia é da encomenda do despacho até o aceite. Ninguém mais escreve ali, nem você.
- `ia/` é sempre sua. Arquivo sem dono: só você atribui o próximo.

Antes de despachar, liste por encomenda:

- arquivos e pastas;
- saídas geradas, inclusive as que os comandos escrevem de passagem, como lock e build;
- recursos exclusivos de `ia/fatos.md › Paralelo`, como porta, banco e diretório de build.

Encomendas com interseção não correm juntas: uma espera a outra. Só conta o que duas execuções simultâneas corromperiam; cache que a ferramenta tolera em paralelo não conta.

## Despacho

- Uma encomenda depende de outra quando precisa de código, saída, decisão ou recurso que a outra produz ou ocupa.
- Despache cada uma assim que as dependências dela forem aceitas. Não espere as outras em curso.
  - Porque: esperar a rodada inteira deixa agentes parados sem proteger nada que as raias já não protejam.
- Ferramenta que só despacha em lote: monte os lotes pelo mesmo critério.

### Fixo primeiro

- Dependência só de interface não põe em fila: com o mesmo `Fixos` nas duas encomendas, quem produz e quem consome correm juntos.
- Quem consome precisa do código para tipar ou importar: uma encomenda curta o materializa antes (tipos, assinaturas, esqueleto exportado).

### Marcos

- Exemplar que outras encomendas vão replicar: aceite-o antes de despachar as réplicas.
- Marco arriscado, como o primeiro molde ou um fixo compartilhado: auditoria antecipada antes das réplicas (`ia/quando/risco.md › Quando`).
- Estado que pede checagens completas: os próximos despachos esperam elas passarem.

## Agregadores

Arquivo que várias encomendas tocariam: índice de reexportação, layout, registro de rotas, configuração central.

- Tem um dono só: uma encomenda de integração, ou a que mais o altera.
- As outras pedem o que precisam em `Pedidos`.
- O dono aplica tudo de uma vez, depois que as que pediram forem aceitas.
- Os conhecidos estão em `ia/fatos.md › Paralelo`.

## Sempre em fila

- Instalação, lock e geração com efeito compartilhado: uma por vez, sem outra encomenda lendo o que elas escrevem.
- Configuração de um mesmo recurso.
- Defeito de causa desconhecida e `executor-5` correm sozinhos.
  - Porque: o diagnóstico ou as garantias deles podem mudar o que as outras precisam fazer.

## Limites

- Respeite o limite de `ia/fatos.md › Paralelo`. Sem vaga, a encomenda espera; o nível não muda.
- Não quebre trabalho coeso para ocupar vagas.
- Ser configuração ou primeira ocorrência não cria dependência por si só.

## Conferência em curso

- Confira cada retorno quando ele chega.
- Comando com escopo pode rodar com outras encomendas em curso, se lê só arquivos já aceitos ou da encomenda conferida.
- Checagens completas, só com nenhuma em execução.
  - Porque: leem a árvore inteira e escrevem build e cache; com encomendas em curso, o resultado mistura trabalho pela metade.

## Ordem típica

Fixos ou fundação, partes independentes em paralelo, marcos antes das réplicas, agregadores, checagens completas.
