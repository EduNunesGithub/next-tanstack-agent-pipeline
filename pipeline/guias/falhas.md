# Falhas

> Para: orquestrador · Leia quando: uma missão falhou ou um achado foi confirmado.

## O que é falha

Uma missão falhou quando:

- devolveu por falta de capacidade;
- uma checagem dela falhou na conferência;
- não cumpriu o `Aceite`;
- escreveu fora da posse, acrescentou supressão ou afrouxou teste;
- quebrou a integração;
- recebeu achado confirmado de causa `implementação`.

## Causa

Antes de corrigir uma falha ou um achado confirmado, classifique a causa. Quem classifica é você.

- Por quê: só você vê ao mesmo tempo a missão, as áreas e o problema. O revisor não recebe a missão, por desenho, e o implementador julgaria o próprio trabalho.

Causas:

- `implementação`: o resultado contraria uma regra, um padrão, um contrato ou um critério que estava claro e ao alcance do implementador, na missão ou nas áreas que ela aciona. Cite o trecho violado e onde ele estava.
- `missão`: a missão omitiu, contradisse ou deixou ambíguo o que o implementador precisava. O erro é seu.
- `pipeline`: uma regra ou instrução faltou, era ambígua, contraditória ou desatualizada, e um implementador competente que a seguisse chegaria ao mesmo resultado.
- `indeterminada`: a evidência não permite escolher entre as anteriores.

Antes de classificar como `indeterminada`, procure em `ocorrencias/` um caso parecido: a segunda ocorrência do mesmo tipo é `pipeline`, porque as instruções não estão evitando o erro.

## Nova tentativa

O caminho vem da causa, não do fato de ter falhado:

- `implementação` com defeito diagnosticado (o quê e onde) → a mesma instância corrige, se disponível; senão, uma missão `t0` de correção. O pedido traz o problema e a evidência, não a solução.
- `implementação` sem diagnóstico depois da conferência, capacidade insuficiente ou segunda falha técnica no mesmo nível → um nível acima (`t0` → `t1` → `t2` → `t3` → `t4`), em instância nova e com `Retentativa`. Em `t4`, mude a abordagem: outra estratégia ou outra divisão.
- `missão` → corrija a missão e reenvie no mesmo nível; não conta como falha do implementador. Ambiguidade do próprio pedido volta para `papeis/orquestrador.md › 2. Desenhe`.
- `pipeline` → mude a regra ou a instrução por `guias/evolucao.md` e registre a ocorrência. O código segue como defeito diagnosticado. Se a mudança aguarda aprovação: `guias/evolucao.md › Enquanto a proposta aguarda`.
- `indeterminada` → o código segue como defeito diagnosticado. Registre a ocorrência com as hipóteses e não mude regra por suposição.
- Ambiente (ferramenta, serviço, credencial, agente indisponível) → bloqueio declarado na entrega. Nunca enfraqueça uma checagem nem troque de agente em silêncio.
- Terceira falha da mesma missão → pare. Entrega parcial com o que funciona, o que falta, por quê e uma recomendação; o que falta vai para `backlog.md` como pendência, para outra sessão retomar.
