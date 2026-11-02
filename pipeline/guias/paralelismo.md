# Paralelismo

> Para: orquestrador · Leia quando: o plano tem duas missões ou mais.

## Posse

- Cada arquivo, pasta, artefato e recurso exclusivo tem um único dono por vez.
- A missão é dona da sua posse desde o despacho até ser aceita. Ninguém mais escreve ali: nem outra missão, nem você.
- `pipeline/` é sua o tempo todo; nenhuma missão a recebe.
- Arquivo sem missão dona fica sob o seu controle: só você atribui o próximo dono.

### Mapa de posse

Antes de despachar, liste para cada missão:

- os arquivos e as pastas;
- os artefatos, inclusive os que os comandos escrevem de passagem, como lock, cache e build;
- os recursos exclusivos de `projeto.md › Paralelismo` que ela usa, como porta, banco e diretório de build.

Duas missões com interseção no mapa não correm ao mesmo tempo: uma passa a depender da outra. Só conta como interseção o artefato que duas execuções simultâneas corromperiam, como lock, build ou banco de testes; cache que a ferramenta tolera em paralelo não conta.

## Despacho por dependência

- Uma missão depende de outra quando precisa de algo que a outra produz: código, artefato gerado, decisão, ou um recurso que a outra ocupa.
- Despache cada missão assim que as dependências dela forem aceitas, sem esperar as demais missões em curso.
  - Por quê: esperar uma onda inteira deixa agentes parados à espera da missão mais lenta, sem proteger nada que o mapa de posse e as dependências já não protejam.
- Se a ferramenta só despacha em lote, monte lotes pelo mesmo critério: entra no lote o que já tem as dependências aceitas.

### Contrato primeiro

- Dependência só de interface não serializa: com o contrato fixado em `Contratos` nas duas missões, produtor e consumidor correm juntos.
- Quando o consumidor precisa do código do contrato para tipar ou importar, uma missão curta o materializa antes (tipos, assinaturas, esqueleto exportado). As outras partem quando ela é aceita.

### Marcos

- Um exemplar que outras missões vão replicar é um marco: aceite-o antes de despachar as réplicas.
- Marco arriscado, como a primeira instância de um padrão ou um contrato compartilhado, passa também por revisão antecipada antes das réplicas (`guias/revisao.md › Quando`).
- Quando um estado integrado exige checagens completas (dependências, configuração das checagens ou contrato compartilhado mudaram), os próximos despachos esperam elas passarem.

## Agregadores

Agregador é um arquivo que várias missões precisariam tocar: índice de reexportação, layout, registro de rotas, configuração central.

- Tem um dono só: uma missão de integração, ou a missão que mais o altera.
- As outras missões pedem o que precisam no campo `Integração` do relato.
- O dono aplica todos os pedidos de uma vez, depois que as missões que pediram forem aceitas.
- Os agregadores conhecidos do projeto estão em `projeto.md › Paralelismo`.

## Sempre em série

- Instalação de dependências, lock e geração com efeitos compartilhados: uma missão por vez, sem outra missão que leia o que elas escrevem.
- Configuração de um mesmo recurso.
- Defeito de causa desconhecida e missão `t4` correm sozinhos.
  - Por quê: o diagnóstico ou as garantias que eles estabelecem podem mudar o que as outras missões precisam fazer.

## Limites

- Respeite o limite de `projeto.md › Paralelismo`. Falta de vaga deixa a missão na fila; não muda o nível dela.
- Contra paralelismo artificial: divida por responsabilidade, cada missão com um resultado próprio verificável. Não quebre um trabalho coeso para ocupar vagas.
- Configurações independentes podem correr em paralelo depois da fundação. Ser configuração ou primeira ocorrência não cria dependência por si só.

## Conferência com missões em curso

- Confira cada relato quando ele chega (`papeis/orquestrador.md › 5. Confira e integre`).
- Comandos com escopo podem rodar enquanto outras missões trabalham, desde que leiam só arquivos já aceitos ou da missão conferida.
- Checagens completas, só com nenhuma missão em execução.
  - Por quê: elas leem a árvore inteira e escrevem artefatos como build e cache; com missões em curso, o resultado mistura trabalho pela metade.

## Ordem típica

Contrato ou fundação → partes independentes em paralelo → marcos antes das réplicas → integração dos agregadores → checagens completas.

- Livre: a ordem e o tamanho dos lotes, dentro destas regras.
