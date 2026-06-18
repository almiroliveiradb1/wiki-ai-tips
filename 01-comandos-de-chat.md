# Claude Code — Comandos de Chat (/)

Comandos de chat integrados ao Claude Code que permitem automação e interação rápida com tarefas comuns.

## Comandos Disponíveis

### `/loop` — Agendador de Tarefas

Agenda uma tarefa para executar em intervalos específicos.

```
/loop cada 30 minutos - executar verificação de dependências
/loop diariamente às 9h - executar testes
/loop a cada 2 horas - fazer backup da configuração
```

**Como funciona:** Você descreve a tarefa e o intervalo em linguagem natural, e o Claude cria um loop de fundo que executa periodicamente.

---

### `/help` — Ajuda Geral

Obtém ajuda sobre comandos disponíveis.

```
/help - lista todos os comandos
/help refactor - ajuda sobre refatoração
/help generate - ajuda sobre geração de código
```

---

### `/clear` — Limpar Histórico

Limpa o histórico da conversa e contexto.

```
/clear - limpa tudo
/clear --keep-files - limpa conversa mas mantém arquivos anexados
```

---

### `/attach` — Anexar Arquivos

Anexa arquivos ou pastas ao contexto da conversa.

```
/attach ./src - anexa pasta src
/attach package.json - anexa arquivo específico
/attach --recursive ./components - anexa com recursão
```

---

### `/search` — Buscar no Código

Busca por termos no codebase.

```
/search "function handleSubmit" - busca função específica
/search --regex "const.*=.*\[\]" - busca com regex
/search --file "*.ts" "interface" - busca em arquivos específicos
```

---

### `/edit` — Editar Código

Abre editor para editar arquivo ou snippet.

```
/edit src/app.ts - edita arquivo
/edit --line 10-20 src/app.ts - edita linhas específicas
```

---

### `/explain` — Explicar Código

Fornece explicação detalhada sobre um trecho de código.

```
/explain - explica seleção atual
/explain src/utils.js - explica arquivo inteiro
/explain --detail high - explicação mais detalhada
```

---

### `/refactor` — Refatorar

Refatora código com foco específico.

```
/refactor - refatora seleção
/refactor --focus performance - refatora com foco em performance
/refactor --focus readability - refatora para melhorar legibilidade
```

---

### `/test` — Gerar Testes

Gera testes automaticamente para código.

```
/test - gera testes para seleção
/test --framework jest - especifica framework
/test --coverage - gera com cobertura
```

---

### `/debug` — Debug Interativo

Inicia modo de debug para investigar problemas.

```
/debug - debug do arquivo/seleção
/debug --interactive - modo interativo completo
/debug --breakpoint 25 - define breakpoint
```

---

### `/lint` — Validação de Código

Valida e sugere melhorias de código.

```
/lint - lint do arquivo atual
/lint --fix - corrige automaticamente
/lint --rules security - apenas regras de segurança
```

---

### `/generate` — Gerar Código

Gera código baseado em descrição natural.

```
/generate componente React com hooks - gera componente
/generate função de validação - gera função
/generate --output utils/helper.ts - especifica saída
```

---

### `/analyze` — Análise de Código

Analisa código identificando problemas.

```
/analyze - analisa arquivo
/analyze --security - análise de segurança
/analyze --performance - análise de performance
```

---

### `/migrate` — Migração

Auxilia migração entre versões/tecnologias.

```
/migrate to typescript - migra para TypeScript
/migrate from react-16 to react-18 - migra framework
```

---

### `/document` — Gerar Documentação

Gera documentação automática.

```
/document - documenta seleção
/document --format markdown - formato específico
/document --include-examples - inclui exemplos
```

---

### `/settings` — Configurações

Acessa configurações do Claude Code.

```
/settings - mostra configurações
/settings model - configura modelo de IA
/settings api-key - configura chave de API
```

---

## Dicas de Uso

- Use `/help [comando]` para obter detalhes específicos
- Combine comandos: `/attach ./src` seguido de `/analyze --security`
- Prefixe com `--` para usar flags específicas
- Use `/loop` para automação recorrente
- Limpe contexto com `/clear` se ficar muito grande

> **Fonte:** DEV Community / Apiyi.com Blog / Claude Code Documentation
