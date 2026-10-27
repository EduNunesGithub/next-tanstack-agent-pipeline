# Escrita da pipeline

> Para o orquestrador, ao escrever em `pipeline/` ou em `AGENTS.md`.

## Onde mora cada informação

- Registros da pipeline: conforme `AGENTS.md` (Onde está a verdade).
- Como rodar, para pessoas: `README.md`.
- Documentação do produto escrita pelo humano: `docs/`, registrada como fonte em `projeto.md`.
- Estrutura, comportamento e configuração: o próprio código. A pipeline não copia nem aponta o que um agente acha lendo o código; cada linha existe porque, sem ela, um agente competente decidiria pior.
- Histórico: `git log`; nenhum arquivo guarda o que já foi feito.

## Estilo

- Estrutura antes de prosa: `##` por área, `###` por entrada, um fato por item.
- Item rotulado: `- Rótulo: valor`, com os rótulos do modelo do arquivo; sub-itens quando o valor tem partes.
- `Por quê:` só quando o motivo não é óbvio; ele diz quando um desvio se justifica.
- Cada regra numa fonte só: frase curta e direta, sem repetir nem resumir o título, outra entrada ou outro arquivo.
- Caminhos, comandos e identificadores entre crases, exatamente como existem e conferidos.
- Só o estado atual: sem datas de progresso, planos ou implementação presumida.
- Tabela só com células curtas; texto longo vai em lista, porque o Prettier alinha as colunas e uma célula longa alarga todas as linhas.
- Títulos estáveis e únicos: fichas e revisões citam a entrada pelo título (`padroes.md › <título>`).
- Antes de acrescentar, procure a entrada que já cobre o assunto e edite-a; entrada que perdeu o objeto sai.

## Normas (`normas.md`)

### Critérios

- Diz o que é obrigatório ou proibido, e por quê.
- É verificável olhando o código.
- Aponta para a fonte da verdade (schema, tema, constantes) em vez de copiar o conteúdo dela.
- Vale para o código do produto e, quando a norma indicar, para arquivos de configuração, respeitando a semântica das ferramentas.
- Se uma funcionalidade comum exige reescrever uma norma, a norma está descrevendo implementação: reescreva-a como limite.
- Exemplos do que cumpre ou viola só entram quando ajudam.
- `Legado:` aponta o código que ainda não cumpre a norma e sai quando não houver mais nenhum.
- Um ID removido não é reaproveitado.
- Normas agrupadas por área (`##`) quando forem várias.

### Modelo

Só os rótulos com conteúdo, nesta ordem. Sem `Checagem:`, a garantia é a revisão; a checagem automática só cabe a norma sem exceção decidida caso a caso.

```markdown
### <ID>: <obrigação ou proibição verificável>

- Por quê: <motivo do limite>
- Escopo: <a que se aplica, quando não é óbvio>
- Como: <detalhe para cumprir>
- Exceção: <caso permitido>
- Checagem: <regra automática que a garante>
- Fonte: <referência existente>
- Legado: <caminho conferido que ainda descumpre a norma>
```

## Padrões (`padroes.md`)

### Critérios

Entra:

- a primeira instância de algo que vai se repetir e em que divergir quebraria a consistência;
- uma decisão que outras tarefas precisam repetir igual;
- qual de duas formas existentes no código é a atual.

Não entra: o que o código já mostra sem ambiguidade, o que uma norma ou uma checagem já garante, uma escolha local, uma intenção ainda não implementada.

### Modelo

Entradas agrupadas por área (`##`):

```markdown
### <nome do padrão>

- Exemplar: `<caminho existente e conferido>`
- Como: <forma ou decisão a repetir; sub-itens quando houver várias>
- Por quê: <o que quebra sem ela>
```

## Projeto (`projeto.md`)

- Só fatos conferidos no destino: não registre como existente, instalado, disponível, confiável ou testado o que não foi conferido.
- Aponte para as fontes reais; não copie o conteúdo delas nem registre uma implementação presumida.
- Estado de adoção: o atual, sem histórico.
- Mudanças de direção seguem `orquestracao.md`.
- Fontes de referência: só as que ficam fora do código ou que uma norma manda registrar, numa `### <área>` por assunto, com itens `` - <papel>: `<caminho>` ``.

## Particularidades (`particularidades.md`)

### Critérios

Entra:

- a armadilha que faria um agente competente errar ou perder tempo;
- a limitação conhecida que pesa numa decisão;
- a decisão cujo motivo o código não mostra.

Não entra: o que o código, a configuração ou a documentação oficial já dizem, a forma a repetir (padrão), a obrigação ou proibição (norma), a operação para pessoas (`README.md`).

### Modelo

Só os rótulos que se aplicam, agrupados por área:

```markdown
## <área>

- Atenção: <armadilha e o que fazer>
- Limitação: <limite e quando ele importa>
- Decisão: <escolha>
  - Por quê: <motivo>
```

## Impactos (`impactos/`)

- Histórico de ocorrências reais desta instalação.
- Arquivo: `impactos/<AAAA-MM-DD>-<assunto>.md`, com a data real.
- Sem incidentes hipotéticos.

```markdown
# <AAAA-MM-DD>: <o que aconteceu>

Causa: <a instrução e por que levou ao problema>

Efeito: <o que se observou>

Correção: <o que mudou na pipeline>
```
