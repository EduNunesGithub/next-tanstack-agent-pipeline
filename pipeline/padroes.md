# Padrões e decisões

> Os exemplares a seguir e as decisões que outras tarefas precisam repetir igual. O orquestrador mantém este arquivo como parte das entregas, a partir do que os implementadores sinalizam em `Registro:`; o humano vê as mudanças no diff e pode vetá-las ao aceitar. Não é norma: dá para desviar quando a tarefa justifica, e então a entrada é atualizada.

Entra aqui:

- a primeira instância de algo que vai se repetir e em que divergir quebraria a consistência;
- uma decisão que outras tarefas precisam repetir igual;
- qual de duas formas existentes no código é a atual.

Não entra: o que o código já mostra sem ambiguidade, o que uma norma ou uma checagem já garante, uma escolha local, uma intenção ainda não implementada.

Formato, uma linha por entrada:

```markdown
- <padrão>: `<caminho existente e conferido>`. <intenção ou decisão a preservar>.
```

## Estado inicial

Nenhum exemplar ou decisão de implementação registrado. As entradas começam depois da primeira implementação conferida neste projeto; não importe exemplares nem decisões de produto do projeto que originou o template.
