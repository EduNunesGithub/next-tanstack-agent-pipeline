# Ficha

A ficha é o pedido completo de um implementador: ele não vê a conversa nem o resto do plano. O orquestrador escreve com as próprias palavras, deixa fora o que não ajuda a executar (inclusive o que `AGENTS.md` já diz) e não deixa nada implícito.

## Modelo

```markdown
Ficha <id> · <nível>
Nível porque: <raciocínio que ainda cabe ao implementador, em uma frase>
Objetivo: <o resultado, em uma frase>
Arquivos: criar <caminhos> · alterar <caminhos>
Artefatos permitidos: <pastas ou arquivos gerados pelos comandos, quando houver>
Ler antes: <exemplar>; normas <IDs>; padrão <entrada de padroes.md>
Contrato: <o que outras partes usam e não pode variar: exports, props, assinaturas, rotas, textos>
Feito quando:

- <critério observável>
- <comando com escopo, de projeto.md>

Livre: <o que o implementador decide>
Fora: <o que não fazer, quando houver risco real de ser feito>
Falha anterior: <só em nova tentativa: o que foi feito, a saída que falhou, o diagnóstico>
```

- `Arquivos` é a lista completa do que pode ser escrito.
- `Artefatos permitidos` delimita saídas geradas, como `node_modules/` numa ficha de instalação. Não autoriza outros arquivos autorais e entra na análise de conflito da onda. Sem esse campo, não há artefatos adicionais permitidos.
- `Contrato` vem em bloco de código quando for código.
- `Ler antes` aponta só para o que existe: sem exemplar, pode indicar uma referência de configuração ou a documentação oficial.
- Em `t0`, `Livre` é `nada; dúvida é bloqueio`.
- Campos sem conteúdo saem.
- O formato do retorno está em `AGENTS.md`.
