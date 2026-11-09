# Falha

Uma encomenda falhou quando:

- devolveu por falta de capacidade;
- não cumpriu `Pronto quando`, ou uma checagem dela falhou na conferência;
- escreveu fora da raia, acrescentou supressão ou afrouxou teste;
- quebrou a integração;
- recebeu um achado confirmado.

## 1. Causa

Classifique antes de corrigir. Quem classifica é você: só você vê a encomenda, as regras e o problema juntos.

- `execução`: o resultado contraria algo claro e ao alcance do executor, na encomenda ou nas regras que ela aciona. Cite o trecho.
- `encomenda`: ela omitiu, contradisse ou deixou ambíguo o que o executor precisava. O erro é seu.
- `pipeline`: uma instrução faltou, era ambígua, contraditória ou velha; um executor competente que a seguisse chegaria ao mesmo resultado.
- `ambiente`: ferramenta, serviço, credencial ou agente indisponível.
- `incerta`: a evidência não decide. Procure o sintoma em `ia/diario.md`: se já está lá, a causa é `pipeline`.

## 2. Caminho

O caminho vem da causa, não do fato de ter falhado.

- `execução`, com defeito diagnosticado (o quê e onde): a mesma instância corrige; sem ela, um `executor-1`. O pedido traz problema e evidência, não a solução.
- `execução` sem diagnóstico, falta de capacidade, ou segunda falha técnica no mesmo nível: um nível acima, instância nova, com `Tentativa anterior`.
  - No `executor-5`: mude a abordagem ou a divisão.
- `encomenda`: corrija e reenvie no mesmo nível. Não conta como falha do executor. Ambiguidade do próprio pedido volta a `ia/fluxo.md › 2. Planeje`.
- `pipeline`: `ia/quando/reparo.md`. O código segue como defeito diagnosticado.
- `incerta`: o código segue como defeito diagnosticado. Registre em `ia/diario.md` com as hipóteses. Não mude regra por suposição.
- `ambiente`: bloqueio declarado na entrega. Nunca enfraqueça uma checagem nem troque de agente em silêncio.

## 3. Limite

Terceira falha da mesma encomenda: pare.

- Entrega `Parcial.`: o que funciona, o que falta, por quê e a sua recomendação.
- O que falta vira pendência, com onde o trabalho parou, para outra sessão retomar.
