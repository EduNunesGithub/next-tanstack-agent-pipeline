# Ficha

A ficha é o pedido completo de um implementador: ele não vê a conversa nem o resto do plano. O orquestrador escreve com as próprias palavras, deixa fora o que não ajuda a executar (inclusive o que `AGENTS.md` já diz) e não deixa nada implícito.

## Modelo

```markdown
Ficha <id> · <nível>
Objetivo: <o resultado, em uma frase>
Arquivos: criar <caminhos> · alterar <caminhos>
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
- `Contrato` vem em bloco de código quando for código.
- Em `t0`, `Livre` é `nada; dúvida é bloqueio`.
- Campos sem conteúdo saem.

## Retorno

```markdown
Status: pronto | bloqueado
Arquivos: <cada arquivo escrito>
Checagens: <comando → resultado>
Decisões: <só as tomadas dentro de Livre>
Registro: <padrão novo, desvio ou norma que atrapalhou; ou nada>
Bloqueio: <o quê, por quê e a sua recomendação>
Resposta: <só quando a ficha pede uma resposta, como numa exploração>
```
