# Ficha

A ficha é o pedido completo de um implementador: ele não vê a conversa nem o resto do plano.

- Escreva com as próprias palavras, conforme `escrita.md`.
- Deixe fora o que não ajuda a executar, inclusive o que `AGENTS.md` já diz.
- Não deixe nada implícito: o que não está na ficha nem na leitura obrigatória o implementador não sabe.

## Modelo

```markdown
Ficha <id> · <nível>
Nível porque: <o julgamento que ainda cabe ao implementador, em uma frase>
Objetivo: <o resultado, em uma frase>
Arquivos: criar <caminhos> · alterar <caminhos>
Artefatos permitidos: <pastas ou arquivos gerados pelos comandos, quando houver>
Ler antes: <exemplar>; padrões <títulos das entradas de padroes.md>; particularidades <áreas>
Contrato: <o que outras partes usam e não pode variar: exports, props, assinaturas, rotas, textos>
Feito quando:

- <critério observável>
- <comando com escopo, de projeto.md>

Livre: <o que o implementador decide>
Fora: <o que não fazer, quando houver risco real de ser feito>
Falha anterior: <só em nova tentativa: o que foi feito, a saída que falhou, o diagnóstico>
```

## Campos

- `Arquivos` é a lista completa do que pode ser escrito. Com `Artefatos permitidos`, é também o que a ficha possui enquanto roda (`orquestracao.md › Donos`).
- `Artefatos permitidos` delimita saídas geradas, como `node_modules/` numa ficha de instalação. Não autoriza arquivos autorais. Sem esse campo, não há artefatos permitidos.
- `Ler antes` aponta só para o que existe. Sem exemplar, pode indicar uma referência de configuração ou a documentação oficial.
- `Contrato` vem em bloco de código quando for código.
- `Livre` é a única liberdade do implementador: o que não está ali é obrigatório ou já decidido. Em `t0`, `Livre` é `nada; dúvida é bloqueio`.
- Campos sem conteúdo saem.
- Ficha de exploração: sem `Arquivos`; `Objetivo` diz o que se quer saber, `Feito quando` descreve a resposta esperada (um resumo, não o código), e o implementador a devolve em `Resposta`.
- O formato do retorno está em `AGENTS.md › Retorno`.
